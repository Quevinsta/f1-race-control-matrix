# Installation

This is currently a development preview.

1. Install Home Assistant and ESPHome.
2. Install/configure the F1 data integration that provides the entities documented in `entities.md`.
3. Add the template sensors from `home-assistant/template-sensors.yaml` to Home Assistant and restart/reload templates.
4. Copy `esphome/secrets.example.yaml` to your ESPHome secrets configuration and replace every placeholder.
5. Review `esphome/f1-race-control.yaml`, especially Home Assistant entity IDs for weather and household sensors. These optional homepage entities may differ in every installation.
6. Compile and flash the ESPHome configuration to the Waveshare ESP32-S3 RGB Matrix controller.
7. In the ESPHome integration for the device, enable permission for the device to perform Home Assistant actions. This is required for the F1TV/Viaplay Sync control.
8. Optionally add `home-assistant/automations.yaml` and change the page-select entity ID to the entity created in your installation.

Before public v1.0, the configuration will be split further so optional homepage/voice features can be disabled more easily.
