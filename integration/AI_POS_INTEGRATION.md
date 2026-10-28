# AI and Google Apps Script POS integration plan

This repository's initial APK build uses the upstream Android cellular/SIP gateway. It does not contain an embedded AI model, a speech service, or a POS adapter yet. The following design is the intended integration boundary; implement and test each part before claiming it works.

## Call and data path

1. Android SIM gateway bridges the cellular call to a SIP endpoint.
2. A separate voice service terminates SIP/RTP and performs streaming speech-to-text.
3. The voice service sends only the minimum required transcript/context to the chosen AI API.
4. Text-to-speech audio is returned to the call.
5. For POS actions, the AI may request a small allowlisted operation such as `lookup_product`, `check_stock`, `create_draft_order`, or `get_order_status`.
6. A server-side adapter validates the operation, caller/business identity, fields, price, and quantities before calling the Google Apps Script web app endpoint.
7. Orders or changes that have financial consequences require explicit customer confirmation and a server-side audit record.

## Security requirements

- Do not embed OpenRouter or any model provider API key in the APK or public repository.
- Do not expose Apps Script deployment secrets in the Android client.
- Keep the POS adapter server-side; use an authenticated HTTPS endpoint and rotate credentials.
- Use a strict allowlist of POS actions, JSON schema validation, rate limits, replay protection, and per-business authorization.
- The AI must not run arbitrary code, SQL, Apps Script functions, or unrestricted URLs.
- Do not record or retain call audio/transcripts unless necessary and appropriately disclosed/consented to.
- Restrict dial-out prefixes and secure the SIP/PBX configuration against toll fraud.
- Never use this experimental gateway for emergency calling.

## Configuration contract (future adapter)

The voice service should read these server-side environment variables; never commit real values:

- `AI_BASE_URL`
- `AI_API_KEY`
- `AI_MODEL`
- `POS_APPS_SCRIPT_URL`
- `POS_SHARED_SECRET`

The Apps Script endpoint should verify authentication, reject unknown operations, validate all inputs, and return structured JSON. The exact request schema must be matched to the user's existing POS before implementation; do not assume its current routes or data model.
