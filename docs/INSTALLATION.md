# Installation / Installatie

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

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
2. Connect the Waveshare ESP32-S3 RGB Matrix board to the HUB75/HUB75E input of the LED panel.
3. Make sure the connector orientation is correct and that you are using the panel's **INPUT**, not its output connector.
4. Connect the panel/controller power according to the Waveshare and panel connections.
5. For the tested setup, a Raspberry Pi 5 27 W USB-C adapter provides sufficient power.

Do not connect or disconnect the HUB75 cable while the setup is powered.

### 2. Prepare Home Assistant

Install and configure your F1 data integration first.

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

<a id="nederlands"></a>

## Nederlands

Deze handleiding neemt je stap voor stap mee van de losse hardware naar een werkende F1 Race Control Matrix in Home Assistant.

### Benodigdheden

- Waveshare ESP32-S3 RGB Matrix-board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB-matrix
- Getest paneel: P2.5, 320×160 mm, 1/32 scan
- 5V-voeding met voldoende stroomcapaciteit
- Een Raspberry Pi 5 27 W USB-C-voedingsadapter is voldoende voor de geteste 128×64-paneelopstelling
- USB-kabel voor de eerste firmware-installatie
- Home Assistant
- ESPHome 2026.9.0
- Een F1-data-integratie in Home Assistant die de benodigde bronentiteiten levert

> Andere HUB75-panelen kunnen een andere scanrate, ander stroomverbruik of andere driver-IC's hebben. De meegeleverde firmware is ingesteld voor de hierboven genoemde hardware.

### 1. Hardware aansluiten

1. Haal de voeding los tijdens het aansluiten.
2. Verbind het Waveshare ESP32-S3 RGB Matrix-board met de HUB75/HUB75E-ingang van het LED-paneel.
3. Controleer de richting van de connector en gebruik de **INPUT** van het paneel, niet de uitgang.
4. Sluit de voeding van paneel/controller aan volgens de aansluitingen van het Waveshare-board en het paneel.
5. Voor de geteste opstelling levert een Raspberry Pi 5 27 W USB-C-adapter voldoende vermogen.

Sluit de HUB75-kabel niet aan of af terwijl de opstelling onder spanning staat.

### 2. Home Assistant voorbereiden

Installeer en configureer eerst je F1-data-integratie.

Het project verwacht de bronentiteiten die in [entities.md](entities.md) staan beschreven, waaronder gegevens voor sessie, baanstatus, timing, rondes en de volgende race.

Kopieer:

`home-assistant/f1_race_control.yaml`

naar:

`/config/packages/f1_race_control.yaml`

Als packages nog niet zijn ingeschakeld, voeg dan dit toe aan `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Controleer de Home Assistant-configuratie en herstart Home Assistant.

Controleer na de herstart of de helpersensoren uit het package aanwezig zijn. De matrix toont timinggegevens van **alleen de top 3 coureurs**.

De optionele `home-assistant/automations.yaml` kan de matrix kort voor een sessie automatisch naar de Race Control-pagina schakelen. Pas vóór gebruik de page-select-entity aan naar die van jouw installatie.

### 3. ESPHome voorbereiden

Kopieer:

`esphome/f1-race-control.yaml`

naar je ESPHome-configuratiemap.

Kopieer daarna:

`esphome/secrets.yaml.example`

naar dezelfde ESPHome-configuratiemap en hernoem het bestand naar:

`secrets.yaml`

Vul je eigen gegevens in:

```yaml
wifi_ssid: "JOUW_WIFI_SSID"
wifi_password: "JOUW_WIFI_WACHTWOORD"
api_encryption_key: "JOUW_32_BYTE_BASE64_SLEUTEL"
```

Genereer een unieke API-encryptiesleutel voor Home Assistant. Zie [SECURITY.md](SECURITY.md) voor de beveiligingsinstellingen.

Commit je echte `secrets.yaml` nooit naar GitHub.

### 4. Valideren en compileren

Open de configuratie in ESPHome en voer eerst **Validate** uit.

Compileer daarna `f1-race-control.yaml`.

De publieke configuratie is gevalideerd met ESPHome 2026.9.0 / ESP-IDF 5.5.5 op de Waveshare ESP32-S3-N32R16.

Controleer bij compileerproblemen eerst of je ESPHome-versie, board en secrets overeenkomen met de gedocumenteerde opstelling.

### 5. Eerste installatie via USB

Installeer de firmware bij een nieuwe Waveshare-controller eerst via USB.

1. Sluit het ESP32-S3-board via USB aan op de computer.
2. Open het apparaat in ESPHome.
3. Kies **Install**.
4. Kies de USB/seriële installatiemethode die in jouw ESPHome-omgeving beschikbaar is.
5. Installeer de gecompileerde firmware.
6. Wacht tot de controller opnieuw is opgestart en verbinding maakt met wifi.

Na de eerste installatie kunnen latere firmware-updates normaal gesproken draadloos via ESPHome worden geïnstalleerd.

### 6. Matrix toevoegen aan Home Assistant

Zodra de controller online is, hoort Home Assistant het ESPHome-apparaat te ontdekken.

Voeg het apparaat toe via de ESPHome-integratie en gebruik de API-encryptiesleutel uit je lokale `secrets.yaml` wanneer daarom wordt gevraagd.

Het apparaat biedt onder andere:

- Power
- Brightness
- F1TV/Viaplay Sync
- Reboot
- Paginaselectie

### 7. Benodigde entiteiten controleren

Open [entities.md](entities.md) en vergelijk de gedocumenteerde bron-/helperentiteiten met jouw Home Assistant-installatie.

Controleer minimaal of sessiestatus, baanstatus, sessietijd, top-3 timing en race-/rondedata beschikbaar zijn waar van toepassing.

Gebruikt jouw F1-integratie andere entity-ID's, pas dan het Home Assistant-package/de templates aan jouw installatie aan.

### 8. F1TV/Viaplay-synchronisatie instellen

Live F1-data en de videostream komen niet altijd exact tegelijk binnen.

Gebruik **F1TV/Viaplay Sync** (`number.f1_live_delay`) om de matrix te vertragen zodat timing- en Race Control-meldingen gelijklopen met de uitzending die je bekijkt.

De ideale vertraging verschilt per omroep, apparaat en stream en moet daarom lokaal worden ingesteld.

### 9. Installatie controleren

Als er geen ondersteunde sessie actief is, hoort de Race Control-pagina `STANDBY` te tonen.

Controleer of:

- de matrix correct opstart;
- Power en Brightness werken;
- paginaselectie werkt;
- de Home Assistant-helpersensoren beschikbaar zijn;
- F1TV/Viaplay Sync de ingestelde vertraging wijzigt;
- de drie coureurregels timingdata kunnen ontvangen;
- ronde-informatie tijdens Race/Sprint verschijnt waar beschikbaar;
- GREEN, YELLOW, RED, VSC, SC en CHEQUERED kunnen worden weergegeven wanneer de F1-databron deze status levert.

Het kwalificatie-eliminatiescherm is experimenteel en moet tijdens live kwalificaties verder worden gevalideerd.

### Later bijwerken

Download/pull een nieuwere versie van `esphome/f1-race-control.yaml`, controleer de changelog en compileer deze in ESPHome. Bestaande installaties kunnen normaal gesproken draadloos worden bijgewerkt.
