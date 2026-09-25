# Installation

## English

This guide takes you from the bare hardware to a working F1 Race Control Matrix in Home Assistant.

### Requirements

- Waveshare ESP32-S3 RGB Matrix board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB matrix
- Tested panel: P2.5, 320×160 mm, 1/32 scan
- 5 V power supply with sufficient current capacity
- A Raspberry Pi 5 27 W USB-C power adapter is sufficient for the tested 128×64 panel setup
- USB cable for the first firmware installation
- Home Assistant
- ESPHome 2026.9.0
- An F1 data integration in Home Assistant that provides the required source entities

> Other HUB75 panels can have different scan rates, power requirements and driver ICs. The supplied firmware is configured for the hardware listed above.

### 1. Connect the hardware

1. Disconnect the power supply while connecting the hardware.
2. Install the Waveshare ESP32-S3 RGB Matrix board **directly onto the HUB75/HUB75E INPUT connector of the LED panel**. No HUB75 ribbon cable is required between the Waveshare board and the panel.
3. Make sure the connector orientation is correct and that the board is connected to the panel's **INPUT**, not its output connector.
4. Connect the USB-C power adapter to the Waveshare board's dedicated **POWER** USB-C connector. **Do not connect the power adapter to the USB connector used for data/programming.**
5. For the tested setup, a Raspberry Pi 5 27 W USB-C adapter provides sufficient power.

Do not connect or disconnect the HUB75 cable while the setup is powered.

### 2. Prepare Home Assistant

Install the **F1 Sensor** custom integration by Nicxe first:

**https://github.com/Nicxe/f1_sensor**

This project uses that integration as its F1 data source. Add it to Home Assistant through **HACS** as a custom repository, install the integration, restart Home Assistant if requested, and then configure F1 Sensor in Home Assistant before continuing with this guide.

The project expects the source entities documented in [entities.md](entities.md), including session, track-status, timing, lap-count and next-race data.

Copy:

`home-assistant/f1_race_control.yaml`

to:

`/config/packages/f1_race_control.yaml`

If Home Assistant packages are not enabled yet, add this to `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Check the Home Assistant configuration and restart Home Assistant.

After the restart, verify that the helper sensors from the package exist. The matrix displays timing data for the **top 3 drivers only**.

The optional `home-assistant/automations.yaml` can automatically switch the matrix to the Race Control page shortly before a session. Change its matrix page-select entity ID to match your installation before enabling it.

### 3. Prepare ESPHome

Copy:

`esphome/f1-race-control.yaml`

to your ESPHome configuration directory.

Then copy:

`esphome/secrets.yaml.example`

to the same ESPHome configuration directory and rename it to:

`secrets.yaml`

Fill in your own values:

```yaml
wifi_ssid: "YOUR_WIFI_SSID"
wifi_password: "YOUR_WIFI_PASSWORD"
api_encryption_key: "YOUR_32_BYTE_BASE64_KEY"
```

Generate a unique Home Assistant API encryption key. See [SECURITY.md](SECURITY.md) for the security setup.

Never commit your real `secrets.yaml` to GitHub.

### 4. Validate and compile

Open the configuration in ESPHome and run **Validate** first.

Then compile `f1-race-control.yaml`.

The public configuration has been validated with ESPHome 2026.9.0 / ESP-IDF 5.5.5 on the Waveshare ESP32-S3-N32R16.

If compilation fails, first check that your ESPHome version, board and secrets match the documented setup.

### 5. First installation over USB

For a new Waveshare controller, install the firmware over USB.

1. Connect the ESP32-S3 board to the computer with USB.
2. Open the device in ESPHome.
3. Choose **Install**.
4. Select the USB/serial installation method available in your ESPHome environment.
5. Install the compiled firmware.
6. Wait for the controller to restart and connect to Wi-Fi.

After the first installation, later firmware updates can normally be installed wirelessly through ESPHome.

### 6. Add the matrix to Home Assistant

Once the controller is online, Home Assistant should discover the ESPHome device.

Add it through the ESPHome integration and enter the API encryption key from your local `secrets.yaml` when requested.

The device exposes controls including:

- Power
- Brightness
- F1TV/Viaplay Sync
- Reboot
- Page selection

### 7. Check the required entities

Open [entities.md](entities.md) and compare the documented source/helper entities with your Home Assistant installation.

At minimum, verify that session status, track status, session time, top-three timing and race/lap data are available where applicable.

If your F1 integration uses different entity IDs, adapt the Home Assistant package/templates to your installation.

### 8. Set the F1TV/Viaplay synchronization

Live F1 data and the video stream do not always arrive at exactly the same time.

Use the **F1TV/Viaplay Sync** control (`number.f1_live_delay`) to delay the matrix so its timing and race-control events line up with the broadcast you are watching.

The ideal delay depends on the broadcaster, device and stream and should therefore be adjusted locally.

### 9. Verify the installation

With no supported session active, the Race Control page should show `STANDBY`.

Check that:

- the matrix starts correctly;
- Power and Brightness work;
- page selection works;
- the Home Assistant helper sensors are available;
- F1TV/Viaplay Sync changes the configured delay;
- the top three driver rows can receive timing data;
- lap information appears during Race/Sprint where available;
- GREEN, YELLOW, RED, VSC, SC and CHEQUERED states can be displayed when supplied by the F1 data source.

The qualifying elimination overlay is experimental and should be validated during live qualifying sessions.

### Updating later

Pull/download the newer `esphome/f1-race-control.yaml`, review the changelog and compile it in ESPHome. Existing installations can normally be updated wirelessly.

---

> 🇳🇱 Nederlandse versie: [INSTALLATION.nl.md](INSTALLATION.nl.md)
