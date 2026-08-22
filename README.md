# Telnyx Verify API (telnyx-verify)

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

Telnyx Verify API is a phone-number verification and two-factor authentication (2FA / OTP) product, paired with Telnyx Number Lookup for number intelligence (carrier, line type, caller name / CNAM, and portability). Verify sends a one-time passcode over **SMS, voice call, flash call, or WhatsApp** and checks the code the user enters — by verification ID or by phone number — using reusable per-channel **Verify Profiles** and message templates, with verification webhooks and built-in anti-fraud controls against SMS pumping and brute-force attacks. **Number Lookup** returns carrier and caller data for an E.164 number for routing, validation, lead enrichment, and fraud workflows.

Both products run on the Telnyx API v2 (`https://api.telnyx.com/v2`) with Bearer API-key authentication.

> **Product-specific treatment.** This entry isolates the Telnyx **Verify + Number Lookup** identity endpoints. The parent company entry [`telnyx`](https://raw.githubusercontent.com/api-evangelist/telnyx/refs/heads/main/apis.yml) documents the full Telnyx cloud-communications (CPaaS) platform — voice, messaging, numbers, fax, wireless, and more. It exists as a dedicated entry because "number verification" is a distinct, high-demand use case (apis.io searches for it were returning zero results).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/telnyx-verify/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/telnyx-verify/refs/heads/main/apis.yml)

## Access Model

- **Access:** Public, self-service. Create a Telnyx account, generate an API v2 key in the Mission Control Portal (Auth / API Keys), and call the endpoints directly — no partner approval or sales gate for standard use.
- **Auth:** Bearer API key — `Authorization: Bearer YOUR_API_KEY`. The same key authenticates Verify, Verify Profiles, and Number Lookup (and the rest of the Telnyx API v2).
- **Pricing:** Pay-as-you-go and usage-metered, no subscription floor. Verify is billed **$0.03 per successful verification plus the channel-delivery cost** (SMS / voice / flash call / WhatsApp) of the message that carries the code. Number Lookup is billed **from $0.0015 per lookup (LRN dip)**; CNAM caller-name may add cost. Volume/committed-use discounts by contacting Telnyx. Confirm current rates on the Telnyx pricing pages before relying on them.
- **Spec:** Telnyx publishes the full API v2 OpenAPI spec openly at [github.com/team-telnyx/openapi](https://github.com/team-telnyx/openapi), and maintains open-source SDKs (telnyx-go, telnyx-node, telnyx-python, …) and a telnyx-mock server that cover these endpoints. The endpoints, single `api.telnyx.com/v2` server, and Bearer (API-key) auth in this repo are grounded in that spec. The OpenAPI schema bodies here summarize request/response fields rather than fully mirroring the published spec — treat the Telnyx spec as authoritative for field-level detail.

## Tags

- Number Verification
- Phone Verification
- OTP
- 2FA
- Lookup
- Verify
- Number Lookup
- CNAM
- Identity
- Anti-Fraud

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Telnyx Verify Verifications API

Trigger and check one-time-passcode verifications. Send a code over SMS, voice call, flash call, or WhatsApp, then verify the code the user entered — by verification ID or by phone number.

- **Human URL:** [https://developers.telnyx.com/docs/identity/verify/quickstart](https://developers.telnyx.com/docs/identity/verify/quickstart)
- **Base URL:** `https://api.telnyx.com/v2`

Endpoints:

- `POST /verifications/sms` — Trigger SMS verification
- `POST /verifications/call` — Trigger Call verification
- `POST /verifications/flashcall` — Trigger Flash call verification
- `POST /verifications/whatsapp` — Trigger WhatsApp verification
- `GET /verifications/by_phone_number/{phone_number}` — List verifications by phone number
- `POST /verifications/by_phone_number/{phone_number}/actions/verify` — Verify code by phone number
- `GET /verifications/{verification_id}` — Retrieve verification
- `POST /verifications/{verification_id}/actions/verify` — Verify code by ID

#### Properties

- [Documentation](https://developers.telnyx.com/docs/identity/verify/quickstart)
- [OpenAPI](openapi/telnyx-verify-openapi.yml)
- [Postman Collection](collections/telnyx-verify.postman_collection.json)
- [Open Collection](collections/telnyx-verify.opencollection.json)

### Telnyx Verify Profiles API

Manage the reusable per-channel configuration applied when sending 2FA messages: create, list, retrieve, update, and delete Verify profiles, plus manage message templates.

- **Human URL:** [https://developers.telnyx.com/docs/identity/verify/quickstart](https://developers.telnyx.com/docs/identity/verify/quickstart)
- **Base URL:** `https://api.telnyx.com/v2`

Endpoints:

- `GET /verify_profiles` — List all Verify profiles
- `POST /verify_profiles` — Create a Verify profile
- `GET /verify_profiles/{verify_profile_id}` — Retrieve Verify profile
- `PATCH /verify_profiles/{verify_profile_id}` — Update Verify profile
- `DELETE /verify_profiles/{verify_profile_id}` — Delete Verify profile
- `GET /verify_profiles/templates` — Retrieve message templates
- `POST /verify_profiles/templates` — Create message template
- `PATCH /verify_profiles/templates/{template_id}` — Update message template

#### Properties

- [Documentation](https://developers.telnyx.com/docs/identity/verify/quickstart)
- [OpenAPI](openapi/telnyx-verify-openapi.yml)
- [Postman Collection](collections/telnyx-verify.postman_collection.json)
- [Open Collection](collections/telnyx-verify.opencollection.json)

### Telnyx Number Lookup API

Number-intelligence lookup returning carrier, line type, caller name (CNAM), and portability data for an E.164 phone number.

- **Human URL:** [https://developers.telnyx.com/docs/identity/number-lookup/quickstart](https://developers.telnyx.com/docs/identity/number-lookup/quickstart)
- **Base URL:** `https://api.telnyx.com/v2`

Endpoints:

- `GET /number_lookup/{phone_number}` — Lookup phone number data (optional `type=carrier` and/or `type=caller-name`)

#### Properties

- [Documentation](https://developers.telnyx.com/docs/identity/number-lookup/quickstart)
- [OpenAPI](openapi/telnyx-verify-openapi.yml)
- [Postman Collection](collections/telnyx-verify.postman_collection.json)
- [Open Collection](collections/telnyx-verify.opencollection.json)

## WebSocket Review

**Does Telnyx Verify API expose a documented public WebSocket API? No.** Verify and Number Lookup are request/response REST over HTTPS. Asynchronous verification results are delivered via **HTTP webhooks** configured on the Verify profile (`webhook_url` / `webhook_failover_url`) — a server-to-endpoint callback, not a client-subscribable WebSocket. No `ws://` or `wss://` endpoint is documented for these products. See [`review.yml`](review.yml).

## Common Properties

- [Domain Security](security/telnyx-verify-domain-security.yml)
- [Authentication](authentication/telnyx-verify-authentication.yml)
- [GitHub Organization](https://github.com/team-telnyx)
- [LinkedIn](https://www.linkedin.com/company/telnyx)
- [Website](https://telnyx.com/products/verify-api)
- [Documentation](https://developers.telnyx.com/docs/identity/verify/quickstart)
- [Plans](plans/telnyx-verify-plans-pricing.yml)
- [Rate Limits](rate-limits/telnyx-verify-rate-limits.yml)
- [Fin Ops](finops/telnyx-verify-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
