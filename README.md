# TecnoCallAgent

**Latest version:** v1.0.0 (first versioned build in progress)  
**Android support:** Android 11+ only in the current upstream baseline; ARM64 (`arm64-v8a`) only. Android 10 and all-device compatibility are not yet verified.

## Install on Android

**Direct APK link (available after the v1.0.0 release build succeeds):**  
[Download TecnoCallAgent v1.0.0 APK](https://github.com/webmike254/TecnoCallAgent/releases/latest/download/TecnoCallAgent-v1.0.0.apk)

If the release download is not available yet, open [GitHub Actions builds](https://github.com/webmike254/TecnoCallAgent/actions), select the newest **Android APK** run, then scroll to the **Artifacts** section and download the APK artifact. Artifacts expire after 30 days; versioned Release APKs are the preferred install link.

### Install steps

1. Open the APK download link on your Android phone.
2. If Android asks, allow your browser to install apps from that source.
3. Open the downloaded APK and tap **Install**.
4. Open TecnoCallAgent and follow its setup instructions. Shizuku and SIP/PBX configuration may be required.
5. Test with a non-critical test call before relying on it.

Android may show a security warning because this is a debug APK, not a Play Store app. Install only if you understand and trust the source.

## What this app does

TecnoCallAgent is being developed from [Voice SIP Agent by sparkcyf](https://github.com/sparkcyf/android-voice-sip-agent). The upstream Android gateway can bridge cellular SIM calls to SIP where the phone's Android version, chipset, firmware, permissions, and audio routing support it.

This initial build pipeline builds the upstream gateway as a baseline. It does **not yet include a completed AI calling brain or a working Google Apps Script POS connector**. Those need to be implemented and tested before advertising the project as an AI receptionist.

## AI and Google Apps Script POS

See [AI/POS integration plan](integration/AI_POS_INTEGRATION.md). The intended architecture uses a separate secured voice service for speech-to-text, an AI provider, text-to-speech, and a server-side adapter for allowlisted POS actions. Do not put API keys or POS secrets inside the APK or this public repository.

## Current limitations

- Upstream baseline minimum Android version: Android 11 (API 30).
- CPU ABI: ARM64 (`arm64-v8a`) only.
- Android 10 support is not enabled simply by lowering minSdk; compatibility work and device tests are needed.
- Cellular audio routing varies by device and may not work on every Tecno model.
- A successful build is not proof that inbound/outbound calls or two-way audio work on a specific phone.
- Do not expose SIP ports publicly without strong authentication and appropriate firewall rules; prevent unauthorized outbound calls and toll fraud.
- Do not use this experimental gateway for emergency calls.

## Build status and version history

- **v1.0.0:** initial versioned APK baseline; only publish/use the direct link once the release workflow succeeds.
- Future releases use version tags such as `v1.0.1`, `v1.1.0`, and `v2.0.0`.

[Open build history and downloadable artifacts](https://github.com/webmike254/TecnoCallAgent/actions) · [Releases](https://github.com/webmike254/TecnoCallAgent/releases)

## License and attribution

This is derived from Voice SIP Agent by sparkcyf. Preserve the upstream license, copyright notices, and third-party notices when copying or distributing its source. Review the upstream [repository](https://github.com/sparkcyf/android-voice-sip-agent) for the applicable license and notices.