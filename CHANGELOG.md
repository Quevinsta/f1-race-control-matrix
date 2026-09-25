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
