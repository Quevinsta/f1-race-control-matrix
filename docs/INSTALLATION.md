# Installation

## Before you start

This project was developed for:

- Waveshare ESP32-S3 RGB Matrix board (ESP32-S3-N32R16)
- 128x64 HUB75/HUB75E panel
- tested P2.5 320x160 mm, 1/32-scan panel
- Home Assistant
- ESPHome 2026.9.0

Do not flash a working device just to test these instructions. A separate controller is the safest way to validate a new installation.

## 1. Home Assistant

Install the F1 data integration you intend to use and verify its entities are available.

Then install `home-assistant/f1_race_control.yaml` as a Home Assistant package. See `home-assistant/README.md`.

## 2. ESPHome secrets

Copy:

`esphome/secrets.yaml.example`

to your ESPHome configuration directory as `secrets.yaml`, then enter your own Wi-Fi credentials.

Never publish your real `secrets.yaml`.

## 3. ESPHome configuration

Copy:

`esphome/f1-race-control.yaml`

to your ESPHome configuration directory.

Validate/compile it before installing.

## 4. First installation

For a new controller, perform the first installation over USB. Later updates can normally be installed over the network.

## 5. Home Assistant permissions

The ESPHome device writes the F1TV/Viaplay Sync value to the Home Assistant entity `number.f1_live_delay`.

In Home Assistant, allow this ESPHome device to perform Home Assistant actions. Without this permission, the sync slider can appear but cannot update the F1 integration's live-delay value.

## 6. Verify

After Home Assistant and the ESPHome device are connected, verify:

- Power and Brightness controls exist.
- F1TV/Viaplay Sync exists.
- Race Control shows STANDBY when no recognized session is active.
- During supported sessions, timing/status data is received.
- The helper sensors from the Home Assistant package are available.

## Notes

The current GitHub configuration is based on the tested V12.6.37 development line. Qualifying elimination overlays remain experimental.
