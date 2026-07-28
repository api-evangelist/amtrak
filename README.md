# Amtrak (amtrak)

Amtrak (the National Railroad Passenger Corporation) is the federally chartered operator of the United States national intercity passenger rail network, headquartered in Washington, D.C. It runs the Northeast Corridor including Acela, the state-supported corridors, the long-distance network, and the Amtrak Thruway Connecting Service bus network, and its published GTFS feed covers 61 routes, 646 stops, 2,948 trips and 20 operating agencies across the United States and into Canada.

In the distribution chain Amtrak sits as a GDS-intermediated supplier of its own inventory: its content reaches third-party booking tools through Travelport Universal API, through Sabre, Apollo and Worldspan on the RailAgent channel, and through rail aggregators including SilverRail, Travelfusion and RailKey Technologies, alongside its own amtrak.com, mobile app and call centre.

Its API posture is honestly stated as one open-standard data feed and nothing else. The only machine-readable contract Amtrak publishes is a static GTFS schedule archive at `content.amtrak.com`, which is completely ungated — no key, no registration, no click-through — but which Amtrak advertises nowhere: there is no developer portal, no documentation page, no OpenAPI, no AsyncAPI, no GraphQL, and no published terms of use for the feed. Everything transactional is closed.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/amtrak/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/amtrak/refs/heads/main/apis.yml)

## Tags

- Travel
- United States
- Rail
- Passenger Rail
- Transit
- GTFS
- Open Data
- Booking
- Distribution
- GDS
- Corporate Travel
- Travel Agents
- Loyalty

## Timestamps

- **Created:** 2026-07-28
- **Modified:** 2026-07-28

## APIs

### Amtrak GTFS Schedule Feed

Amtrak's complete national timetable published as a static General Transit Feed Specification archive, served from `content.amtrak.com` with no registration, no API key, no click-through licence and no rate limit. The edition harvested on 2026-07-28 carries `feed_version` 20260727 and holds 8 GTFS files — `agency`, `calendar`, `feed_info`, `routes`, `shapes`, `stops`, `stop_times` and `trips` — covering 20 agencies, 61 routes (49 rail and 12 bus by `route_type`), 646 stops, 2,948 trips, 37,862 stop times and 373,236 shape points, with calendar service dates spanning 20260726 to 20270726.

`feed_info` declares `feed_publisher_name` Amtrak and a first-party contact address of `DL_DTGTFSsupport@Amtrak.com`. This is the only machine-readable contract Amtrak publishes, and Amtrak publishes no page describing it — the URL is discoverable only through third-party registries such as the Mobility Database and Transitland.

- **Human URL:** [https://mobilitydatabase.org/feeds/gtfs/mdb-11](https://mobilitydatabase.org/feeds/gtfs/mdb-11)
- **Base URL:** `https://content.amtrak.com/content/gtfs/GTFS.zip`

#### Tags

- GTFS
- Schedules
- Timetables
- Transit
- Open Data
- Rail

#### Properties

- [GTFS](gtfs/amtrak-gtfs.zip) — [General Transit Feed Specification](https://gtfs.org/documentation/schedule/reference/)
- [Download](https://content.amtrak.com/content/gtfs/GTFS.zip)
- [Specification](https://gtfs.org/documentation/schedule/reference/)
- [Registry](https://mobilitydatabase.org/feeds/gtfs/mdb-11) — Mobility Database mdb-11
- [Registry](https://www.transit.land/operators/o-9-amtrak) — Transitland o-9-amtrak
- [Email](mailto:DL_DTGTFSsupport@Amtrak.com)

## Common Properties

- [Website](https://www.amtrak.com/)
- [Newsroom](https://media.amtrak.com/)
- [Travel Agent Portal](https://portal.railagent.com/)
- [GitHub Organization](https://github.com/Amtrak)
- [LinkedIn](https://www.linkedin.com/company/amtrak)

## Switching Cost

The full switching-cost analysis — interface shape, second source, exit path, identifier portability, contractual lock-in, access gate and distribution model — lives in [`review.yml`](review.yml).

| Dimension | Value |
| --- | --- |
| Interface shape | `open-standard` (GTFS static) — scoped to schedules only; everything transactional is `none-published` |
| Second source | `no-alternative` for Amtrak seat inventory; multiple channels to the same inventory |
| Exit path | `no-export-published` |
| Identifier portability | GTFS keys with Amtrak three-letter station codes as `stop_id` / `stop_code`; Amtrak-internal numeric `route_id` / `trip_id` |
| Contractual lock-in | Nothing published first-party — `www.amtrak.com` returns 403 to every non-browser client |
| Access gate | `commercial-agreement` (accreditation, test-case worksheet, three-week UAT via Travelport) |
| Distribution model | `gds-intermediated` |
| NDC posture | Not applicable — rail operator; no IATA NDC and no UIC OSDM reference found |

## Maintainers

- Kin Lane — kin@apievangelist.com
