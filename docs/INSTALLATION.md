# Installation / Installatie

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

## English

### Requirements

This project is developed and validated for:

- Waveshare ESP32-S3 RGB Matrix board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB matrix
- Tested panel: P2.5, 320×160 mm, 1/32 scan
- Regulated 5 V power supply sized for the panel and controller
- Home Assistant
- ESPHome 2026.9.0

### 1. Prepare Home Assistant

Install and configure the F1 data integration that provides the source entities listed in [entities.md](entities.md).

Copy `home-assistant/f1_race_control.yaml` to:

`/config/packages/f1_race_control.yaml`

Enable packages in `configuration.yaml` if required:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Check the Home Assistant configuration and restart Home Assistant.

The optional `home-assistant/automations.yaml` switches the matrix to F1 Race Control shortly before a session. Change its matrix page-select entity ID to match your installation before using it.

### 2. Configure ESPHome secrets

Copy:

`esphome/secrets.yaml.example`

to your ESPHome configuration directory as `secrets.yaml`.

Replace every placeholder with your own values. Generate a unique API encryption key as described in [SECURITY.md](SECURITY.md). Never commit your real `secrets.yaml`.

### 3. Install the ESPHome configuration

Copy:

`esphome/f1-race-control.yaml`

to your ESPHome configuration directory.

Validate and compile it before installation.

For a new controller, perform the first installation over USB. Later updates can normally be installed over the network.

### 4. Add the device to Home Assistant

Add the ESPHome device to Home Assistant and use the API encryption key from your local `secrets.yaml` when requested.

The matrix exposes Power, Brightness, F1TV/Viaplay Sync and Reboot controls.

### 5. Verify the installation

Verify that:

- the matrix starts correctly;
- Power and Brightness are available;
- F1TV/Viaplay Sync follows `number.f1_live_delay`;
- Race Control shows `STANDBY` when no recognized session is active;
- the helper sensors from the Home Assistant package are available;
- live session, timing, lap and track-status data appear during a supported session.

The qualifying elimination overlay remains experimental and should be validated during live qualifying sessions.

---

<a id="nederlands"></a>

## Nederlands

### Benodigdheden

Dit project is ontwikkeld en gevalideerd voor:

- Waveshare ESP32-S3 RGB Matrix-board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB-matrix
- Getest paneel: P2.5, 320×160 mm, 1/32 scan
- Gestabiliseerde 5V-voeding die voldoende vermogen levert voor paneel en controller
- Home Assistant
- ESPHome 2026.9.0

### 1. Home Assistant voorbereiden

Installeer en configureer de F1-data-integratie die de bronentiteiten uit [entities.md](entities.md) levert.

Kopieer `home-assistant/f1_race_control.yaml` naar:

`/config/packages/f1_race_control.yaml`

Schakel packages zo nodig in via `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Controleer de Home Assistant-configuratie en herstart Home Assistant.

De optionele `home-assistant/automations.yaml` schakelt het paneel kort voor een sessie automatisch naar F1 Race Control. Pas vóór gebruik de page-select-entity aan naar de entity van jouw installatie.

### 2. ESPHome-secrets instellen

Kopieer:

`esphome/secrets.yaml.example`

naar je ESPHome-configuratiemap als `secrets.yaml`.

Vervang alle placeholders door je eigen waarden. Genereer een unieke API-encryptiesleutel zoals beschreven in [SECURITY.md](SECURITY.md). Commit je echte `secrets.yaml` nooit naar Git.

### 3. ESPHome-configuratie installeren

Kopieer:

`esphome/f1-race-control.yaml`

naar je ESPHome-configuratiemap.

Valideer en compileer de configuratie vóór installatie.

Voer bij een nieuwe controller de eerste installatie via USB uit. Latere updates kunnen normaal gesproken via het netwerk worden geïnstalleerd.

### 4. Apparaat toevoegen aan Home Assistant

Voeg het ESPHome-apparaat toe aan Home Assistant en gebruik de API-encryptiesleutel uit je lokale `secrets.yaml` wanneer daarom wordt gevraagd.

De matrix biedt Power, Brightness, F1TV/Viaplay Sync en Reboot als bediening.

### 5. Installatie controleren

Controleer of:

- de matrix correct opstart;
- Power en Brightness beschikbaar zijn;
- F1TV/Viaplay Sync `number.f1_live_delay` volgt;
- Race Control `STANDBY` toont wanneer geen ondersteunde sessie actief is;
- de helpersensoren uit het Home Assistant-package beschikbaar zijn;
- tijdens een ondersteunde sessie live sessie-, timing-, ronde- en baanstatusdata verschijnen.

Het kwalificatie-eliminatiescherm is nog experimenteel en moet tijdens live kwalificaties verder worden gevalideerd.
