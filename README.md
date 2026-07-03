# ClassPass (classpass)

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
