# Home Assistant entities / Home Assistant-entiteiten

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

## English

The ESPHome firmware expects the following source entities from the connected Home Assistant F1 integration:

- `sensor.f1_current_session`
- `sensor.f1_session_status`
- `sensor.f1_track_status`
- `sensor.f1_session_time_remaining`
- `sensor.f1_race_lap_count`
- `sensor.f1_next_race`
- `sensor.f1_top_three_p1`
- `sensor.f1_top_three_p2`
- `sensor.f1_top_three_p3`
- `sensor.f1_driver_positions`
- `number.f1_live_delay`

The supplied Home Assistant package creates compact helper entities used by ESPHome:

- `sensor.f1_race_p1`
- `sensor.f1_race_p2`
- `sensor.f1_race_p3`
- `sensor.f1_eliminated_1` through `sensor.f1_eliminated_6`

The F1 data integration itself is not included in this repository. Entity availability and attributes depend on the integration connected by the user.

---

<a id="nederlands"></a>

## Nederlands

De ESPHome-firmware verwacht de volgende bronentiteiten van de gekoppelde F1-integratie in Home Assistant:

- `sensor.f1_current_session`
- `sensor.f1_session_status`
- `sensor.f1_track_status`
- `sensor.f1_session_time_remaining`
- `sensor.f1_race_lap_count`
- `sensor.f1_next_race`
- `sensor.f1_top_three_p1`
- `sensor.f1_top_three_p2`
- `sensor.f1_top_three_p3`
- `sensor.f1_driver_positions`
- `number.f1_live_delay`

Het meegeleverde Home Assistant-package maakt compacte helpers aan die door ESPHome worden gebruikt:

- `sensor.f1_race_p1`
- `sensor.f1_race_p2`
- `sensor.f1_race_p3`
- `sensor.f1_eliminated_1` t/m `sensor.f1_eliminated_6`

De F1-data-integratie zelf maakt geen deel uit van deze repository. Welke entiteiten en attributen beschikbaar zijn, hangt af van de integratie die de gebruiker koppelt.
