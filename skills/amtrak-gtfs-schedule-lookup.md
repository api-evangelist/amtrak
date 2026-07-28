---
name: amtrak-gtfs-schedule-lookup
description: Fetch, parse and query the Amtrak GTFS Schedule Feed to answer "what trains serve this station", "what is the timetable for this route" and "which days does this trip run" - the only public Amtrak contract, with no key and no registration.
api: gtfs/amtrak-gtfs.zip
contract: https://content.amtrak.com/content/gtfs/GTFS.zip
contract_type: GTFS Schedule (static)
grounding: >-
  Grounded in the harvested archive gtfs/amtrak-gtfs.zip (feed_version 20260727)
  and the live response headers of content.amtrak.com. Amtrak publishes no
  OpenAPI, so there are no operationIds; the operations below are the real files
  and real columns present in the archive.
operations:
  - GET https://content.amtrak.com/content/gtfs/GTFS.zip
  - read feed_info.txt
  - read agency.txt
  - read routes.txt
  - read stops.txt
  - read calendar.txt
  - read trips.txt
  - read stop_times.txt
  - read shapes.txt
generated: '2026-07-28'
method: generated
---

# Amtrak GTFS schedule lookup

Amtrak publishes one machine-readable contract and advertises it nowhere. This skill is how an agent uses it correctly.

## 1. Fetch

```
GET https://content.amtrak.com/content/gtfs/GTFS.zip
```

No API key. No registration. No click-through. No `Referer` or `User-Agent` requirement. The response is `application/zip`, roughly 19 MB (19,244,661 bytes on 2026-07-28).

Do **not** fetch the consumer site to get schedules. `www.amtrak.com` refuses every non-browser client, and `api.amtrak.com` answers `401` on every path.

## 2. Poll politely

Amtrak sends `Cache-Control: max-age=0, no-cache, no-store`, but it also sends a stable `ETag` and `Last-Modified`. Conditional GET is the **only** change-detection mechanism that exists — there is no changelog, no version endpoint and no notification channel.

```
GET /content/gtfs/GTFS.zip
If-None-Match: "cad0fde23bb090325a0626519c0fdfd6:1785164405.67323"
```

A `304` means nothing changed. Amtrak publishes no rate limit; the feed's `feed_version` datestamp moves roughly weekly, so once a day is generous and once an hour is abuse. Do not re-download 19 MB on every user query — cache the parsed tables and re-check with a conditional HEAD.

## 3. Parse

Eight CSV members, comma-separated, UTF-8 **with a byte-order mark**. Use a BOM-tolerant reader (`encoding='utf-8-sig'` in Python) or the first column name of every file will come back corrupted.

| File | Rows (20260727) | Key |
|---|---|---|
| `feed_info.txt` | 1 | — |
| `agency.txt` | 20 | `agency_id` |
| `routes.txt` | 61 | `route_id` |
| `stops.txt` | 646 | `stop_id` |
| `calendar.txt` | 403 | `service_id` |
| `trips.txt` | 2,948 | `trip_id` |
| `stop_times.txt` | 37,862 | `trip_id` + `stop_sequence` |
| `shapes.txt` | 373,236 | `shape_id` + `shape_pt_sequence` |

Validate against `json-schema/amtrak-gtfs-schema.json`. The entity graph and every foreign key is in `data-model/amtrak-data-model.yml`.

## 4. Query

**Which trains serve a station?** Station codes are the familiar Amtrak three-letter codes, and Amtrak puts the same value in both `stop_id` and `stop_code` (`CHI`, `ABE`, `ABQ`).

```
stop_times WHERE stop_id = 'CHI'
  -> join trips ON trip_id
  -> join routes ON route_id      # route_long_name is the train's name
  -> join calendar ON service_id  # which weekdays it runs
```

**What is a route's timetable?** `route_short_name` is empty in every Amtrak row — identity lives entirely in `route_long_name` (`Acela`, `California Zephyr`, `Coast Starlight`, `Amtrak Thruway Connecting Service`, 48 distinct names in all). Match on `route_long_name`, then walk `trips` → `stop_times` ordered by `stop_sequence`.

**Which train number is this?** `trips.trip_short_name` is the public Amtrak train number (`307`, `341`, `392`) — the identifier a passenger recognises and the key every downstream tracking project joins on. `route_id`, `trip_id`, `service_id` and `agency_id` are opaque Amtrak-internal integers with no external meaning; never surface them to a user and never assume they are stable between editions.

**Is it a train or a bus?** `routes.route_type` is `2` for the 49 rail routes and `3` for the 12 Amtrak Thruway Connecting Service bus routes. Amtrak's feed mixes them. If the user asked for a train, filter `route_type = 2`.

**Does it run on a given date?** Join `calendar` on `service_id`, check the weekday flag and that the date falls inside `start_date`/`end_date`. Amtrak ships **no** `calendar_dates.txt`, so there are no holiday exceptions in the feed — a service that `calendar` says runs may still be cancelled in reality, and the feed will not tell you.

**Times past midnight.** GTFS times may exceed `23:59:59` (`25:10:00` means 1:10 am the following service day). Do not parse with a naive time type.

## 5. Know the limits before you answer a user

- **Schedules only.** There is no realtime feed. `GTFS-RT-TripUpdates.pb`, `GTFS-RT-VehiclePositions.pb` and `GTFS-RT-Alerts.pb` all 404 on `content.amtrak.com`. Never state a train's actual position or delay from this data — it is a timetable, not a status.
- **No fares.** No `fare_attributes`, `fare_rules` or GTFS-Fares v2 files. This feed cannot price a journey.
- **No availability, no booking.** Nothing in this contract can check a seat, hold, book, pay, ticket, change or refund. Those capabilities are reached only through an accredited intermediary (Travelport, Sabre, SilverRail, Travelfusion, RailKey) after an Amtrak accreditation and a three-week UAT.
- **Validity window.** `feed_info` declares `feed_start_date` 20260728 and `feed_end_date` 20260803 — one week — even though `calendar` reaches 20270726. Treat anything beyond the declared window as provisional and re-fetch.
- **Licence.** Amtrak attaches no terms, licence or attribution requirement to this file and publishes no page describing it. The only statement of its terms anywhere is a FOIA-disclosed sentence, and it is conditional. Do not tell a user this is open data under a named licence, because it is not.

## 6. Escalate

The one first-party support channel is the address declared inside the feed: `DL_DTGTFSsupport@Amtrak.com` (`feed_info.feed_contact_email`). It appears nowhere on amtrak.com.

## Related artifacts

- `conventions/amtrak-conventions.yml` — transport, caching, encoding, identifiers
- `authentication/amtrak-authentication.yml` — none, verified
- `lifecycle/amtrak-lifecycle.yml` — versioning and freshness
- `conformance/amtrak-conformance.yml` — what the feed does and does not conform to
- `packages/amtrak-packages.yml` — community libraries, all unofficial
