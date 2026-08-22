# ClassPass (classpass)

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

ClassPass is a fitness and wellness marketplace that lets consumers book classes, gym visits, and spa/wellness experiences across a network of studios in a single app using a monthly credit subscription. On the supply side, ClassPass runs a partner integration platform - centered on a named "ClassPass Inventory API" - that lets studios and their scheduling/booking software (100+ platforms, including Mindbody, Vagaro, Zen Planner, and Eversports Manager) push live class schedules, availability, and pricing to ClassPass and receive bookings and cancellations back. The partner developer portal at developers.classpass.com requires an approved partner login (Auth0) to view the API specification document and run certification tests; ClassPass does not publish a public, unauthenticated API reference, OpenAPI file, or Postman collection. ClassPass is now part of Playlist, the group formed together with Mindbody and Booker.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/classpass/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/classpass/refs/heads/main/apis.yml)

## Access model - honest summary

ClassPass does **not** have a public, self-serve developer API. There is a real developer/partner portal (`developers.classpass.com`), and a page on it titled "ClassPass Inventory API" (`/specInfo`), but the entire portal is an Auth0-gated Next.js application - the page's initial HTML/JSON ships with empty state and a login redirect (`AUTH0_DOMAIN: core-portal.auth0.com`); no endpoint list, request/response schema, or OpenAPI file is visible without an approved partner account. A separate ClassPass Help Center article, ["What is ClassPass's API Access Terms of Use?"](https://help.classpass.com/hc/en-us/articles/360061293531-What-is-ClassPass-s-API-Access-Terms-of-Use), confirms API access is governed by its own terms, consistent with a gated, partner-application model rather than an open developer program.

What ClassPass does document publicly, through partner-marketing pages and its integration partners' own help centers, is the *shape* of the integration:

- Studios connect their scheduling/booking software (100+ supported platforms) to ClassPass.
- The studio's system pushes class schedules, real-time availability, and pricing to ClassPass.
- ClassPass pushes bookings and cancellations back to the studio's system (observed by at least one partner platform to reconcile on a roughly 30-minute cycle).
- "SmartTools" (SmartRate for dynamic credit pricing, SmartSpot for inventory/placement) sit on top of this same data pipe to help studios optimize fill rate and payout.
- There is no upfront cost for a studio to list on ClassPass; ClassPass pays studios via Tipalti against a confidential, partner-negotiated rate floor, adjusted upward in real time by SmartRate.

No endpoint paths, base URLs, authentication flow details, or payload schemas are published outside the gated portal, so none are fabricated here. The two entries under `apis` in `apis.yml` document the two things that are independently verifiable (the named "ClassPass Inventory API" product and the observable shape of the gating/certification portal itself), each explicitly flagged `endpointsModeled: false`.

## Tags

- Fitness
- Wellness
- Class Booking
- Marketplace
- Studios
- Gyms
- Scheduling
- Partner API

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### ClassPass Inventory API

ClassPass's named partner integration API for studios and their scheduling/booking software. Studios push class schedules, real-time availability, and pricing to ClassPass, and receive bookings and cancellations back. The API's own reference document lives behind an Auth0-gated partner login; no endpoint paths are modeled here (`endpointsModeled: false`).

- **Human URL:** [https://developers.classpass.com/specInfo](https://developers.classpass.com/specInfo)

#### Tags

- Inventory
- Classes
- Schedules
- Availability
- Bookings

#### Properties

- [Documentation](https://developers.classpass.com/)
- [API Reference](https://developers.classpass.com/specInfo) (Auth0 login required to view spec content)

### ClassPass Partner Certification & Token Portal

The client-side application shell served at `developers.classpass.com` declares Redux state entities named `cpToken`, `integratorSettings`, `specDoc`, `validationTests`, and `runTest` - evidence the portal issues partner API tokens, stores per-integrator settings, serves the gated spec document, and runs an automated certification test suite integrations must pass before going live. No further technical detail is publicly visible without an approved partner account.

- **Human URL:** [https://developers.classpass.com/](https://developers.classpass.com/)

#### Tags

- Partner Portal
- OAuth
- Certification
- Sandbox

#### Properties

- [Documentation](https://developers.classpass.com/)

## Common Properties

- [Website](https://classpass.com)
- [LinkedIn](https://www.linkedin.com/company/classpass)
- [Developer Portal](https://developers.classpass.com/)
- [Help Center - API Access Terms of Use](https://help.classpass.com/hc/en-us/articles/360061293531-What-is-ClassPass-s-API-Access-Terms-of-Use)
- [Booking Integrations](https://classpass.com/partners/classpass-booking-integrations)
- [Plans](plans/classpass-plans-pricing.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
