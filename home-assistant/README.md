# F1 Race Control Matrix — Home Assistant

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

## English

This directory contains the Home Assistant helper package and optional automation used by the ESPHome firmware.

### Install the helper package

1. Create `/config/packages/` if it does not exist.
2. Copy `f1_race_control.yaml` to `/config/packages/f1_race_control.yaml`.
3. Enable packages in `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

4. Check the Home Assistant configuration and restart Home Assistant.
5. Confirm these helper entities exist:
   - `sensor.f1_race_p1`
   - `sensor.f1_race_p2`
   - `sensor.f1_race_p3`
   - `sensor.f1_eliminated_1` through `sensor.f1_eliminated_6`

The helper package expects `sensor.f1_driver_positions` and `sensor.f1_session_time_remaining`. The ESPHome firmware uses additional source entities documented in `docs/entities.md`.

### Optional automation

`automations.yaml` can switch the matrix to F1 Race Control shortly before a session. Change `select.waveshare_matrix_select_page` to the page-select entity created by your own matrix before enabling the automation.

The F1 data integration itself is not included in this repository.

---

<a id="nederlands"></a>

## Nederlands

Deze map bevat het Home Assistant-helperpackage en een optionele automatisering voor de ESPHome-firmware.

### Helperpackage installeren

1. Maak `/config/packages/` aan als deze map nog niet bestaat.
2. Kopieer `f1_race_control.yaml` naar `/config/packages/f1_race_control.yaml`.
3. Schakel packages in via `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

4. Controleer de Home Assistant-configuratie en herstart Home Assistant.
5. Controleer of deze helpers bestaan:
   - `sensor.f1_race_p1`
   - `sensor.f1_race_p2`
   - `sensor.f1_race_p3`
   - `sensor.f1_eliminated_1` t/m `sensor.f1_eliminated_6`

Het helperpackage verwacht `sensor.f1_driver_positions` en `sensor.f1_session_time_remaining`. De ESPHome-firmware gebruikt daarnaast de bronentiteiten uit `docs/entities.md`.

### Optionele automatisering

`automations.yaml` kan de matrix kort voor een sessie naar F1 Race Control schakelen. Vervang `select.waveshare_matrix_select_page` door de page-select-entity van je eigen matrix voordat je de automatisering inschakelt.

De F1-data-integratie zelf is niet inbegrepen in deze repository.
