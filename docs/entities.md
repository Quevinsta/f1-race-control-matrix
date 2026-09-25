# Home Assistant entities

The firmware currently expects these F1 entities from the connected Home Assistant F1 integration:

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

The supplied Home Assistant templates create compact entities consumed by ESPHome:

- `sensor.f1_race_p1`
- `sensor.f1_race_p2`
- `sensor.f1_race_p3`
- `sensor.f1_eliminated_1` through `sensor.f1_eliminated_6`

The current development firmware also contains optional homepage entities for weather, outdoor temperature, room temperature and waste collection. These are installation-specific and will be made modular before the public v1.0 release.
