# Changelog

## 0.1.0-private-preview - 2026-09-25

- Initial private GitHub project structure.
- Added sanitized ESPHome development configuration based on V12.6.37.
- Added Home Assistant race-position and qualifying-elimination template sensors.
- Added automatic page switch five minutes before a session.
- Added example ESPHome secrets.
- Added hardware, installation and entity documentation.
- Added project disclaimer and MIT license.

### Experimental

- Qualifying elimination overlay.
- Sprint Qualifying elimination behavior still requires live-session validation.

## Firmware cleanup RC1

- Removed Voice Assistant / Jarvis code from the public firmware candidate.
- Removed household-specific homepage rendering and sensors.
- Public candidate now boots directly into F1 Race Control.
- Retained Race/Sprint timing, qualifying labels, flags, elimination overlay, F1TV/Viaplay Sync, standby and the 10-minute post-session hold.
- Credentials remain externalized through ESPHome secrets.
- RC1 must compile successfully before it is promoted to the repository's main firmware file.

### RC1 validation

- YAML validation passed with ESPHome 2026.9.0.
- Full ESP-IDF compilation succeeded on 2026-09-25.
- Firmware image size: 713,003 bytes.
- DIRAM usage: 106,419 / 341,760 bytes (31.1%).
- Flash usage: 713,003 / 16,515,072 bytes (4.3%).
- No firmware was flashed to the development panel during this validation.
