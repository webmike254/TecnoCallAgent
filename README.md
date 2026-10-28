# TecnoCallAgent

Independent working fork of [Voice SIP Agent](https://github.com/sparkcyf/android-voice-sip-agent), intended to connect an Android SIM gateway to an AI voice agent and a Google Apps Script POS.

## Project status

- Upstream baseline: v0.3.5 (GPL-2.0-or-later with Apache-2.0 linking exception).
- Upstream currently targets Android 11+ (API 30) and ARM64. Android 10 support is not yet implemented or verified.
- Calls are routed through SIP/PBX; this Android app is not itself an AI model or a POS backend.
- Device-specific call audio routing is experimental. Do not rely on it for emergency calls.
- This repository must retain upstream license and third-party notices.

## Planned integration architecture

```text
Android SIM gateway
       | SIP / call audio
       v
Voice bridge / speech service
       | speech-to-text -> AI provider -> text-to-speech
       v
POS adapter (server-side Apps Script endpoint)
       | HTTPS + authentication + schema validation
       v
Google Apps Script POS
```

Never put OpenRouter/AI provider keys, Apps Script admin secrets, or long-lived POS credentials in the Android APK. Keep secrets server-side, authenticate every request, validate phone numbers and order fields, and require confirmation before placing or changing orders. The AI must not be able to invoke arbitrary POS functions.

## Build

The upstream project includes native PJSIP dependencies. Follow its `README.md`, `TECHNICAL.md`, and `sip-pjsua2/native/build-pjsua2.sh` instructions. GitHub Actions build artifacts will be published only after the build workflow succeeds. An artifact is not a verified working phone gateway until tested on a physical device.

## Device support

The upstream baseline requires Android 11+ and arm64-v8a. Lowering `minSdk` alone cannot provide Android 10 support: Telecom roles, hidden APIs, Shizuku operations, and call-audio routing must be audited and guarded. Supported devices will be documented only after testing inbound calls, outbound calls, and two-way audio.

## Upstream attribution and license

Copyright notices from the upstream project and its dependencies must be preserved. This project is derived from Voice SIP Agent by sparkcyf. See `LICENSE` and `THIRD_PARTY_NOTICES.md` for the full license and notices.
