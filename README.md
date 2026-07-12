# Telnyx Verify API (telnyx-verify)

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
