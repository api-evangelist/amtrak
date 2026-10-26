# Amtrak (amtrak)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
- [Newsroom](https://media.amtrak.com/) — [RSS](https://media.amtrak.com/rss/)
- [Web Notices and Site Terms of Use](https://media.amtrak.com/terms-of-use/) — the only first-party Amtrak terms reachable by a non-browser client
- [Privacy Policy](https://media.amtrak.com/privacy-policy/)
- [Travel Agent Portal](https://portal.railagent.com/)
- [GitHub Organization](https://github.com/Amtrak)
- [LinkedIn](https://www.linkedin.com/company/amtrak)

## Artifacts

Everything below was derived from the harvested GTFS archive or probed live on 2026-07-28. Amtrak publishes none of it.

| Artifact | File | Method |
| --- | --- | --- |
| Authentication | [`authentication/amtrak-authentication.yml`](authentication/amtrak-authentication.yml) | probed — none required |
| API conventions | [`conventions/amtrak-conventions.yml`](conventions/amtrak-conventions.yml) | derived |
| Lifecycle | [`lifecycle/amtrak-lifecycle.yml`](lifecycle/amtrak-lifecycle.yml) | derived |
| Conformance | [`conformance/amtrak-conformance.yml`](conformance/amtrak-conformance.yml) | derived |
| Data model | [`data-model/amtrak-data-model.yml`](data-model/amtrak-data-model.yml) | derived |
| JSON Schema | [`json-schema/amtrak-gtfs-schema.json`](json-schema/amtrak-gtfs-schema.json) | derived |
| Packages | [`packages/amtrak-packages.yml`](packages/amtrak-packages.yml) | searched — zero official, four community |
| llms.txt | [`llms/amtrak-llms.txt`](llms/amtrak-llms.txt) | generated |
| Agent skill | [`skills/amtrak-gtfs-schedule-lookup.md`](skills/amtrak-gtfs-schedule-lookup.md) | generated |
| Well-known | [`well-known/amtrak-well-known.yml`](well-known/amtrak-well-known.yml) | searched — nothing published on any host |
| Domain security | [`security/amtrak-domain-security.yml`](security/amtrak-domain-security.yml) | probed |

Deliberately absent, because Amtrak publishes no such thing: OpenAPI, AsyncAPI, GraphQL, webhooks, MCP server, SDKs, CLI, sandbox, changelog, status page, deprecation policy, vulnerability disclosure programme, trust centre, OAuth scopes and Postman collection. `trust.`, `security.` and `status.amtrak.com` are NXDOMAIN; `/.well-known/security.txt` is 404 or 401 on every resolving host.

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
