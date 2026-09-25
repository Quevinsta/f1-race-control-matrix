# F1 Race Control Matrix

This directory contains the Home Assistant helper package required by the ESPHome firmware.

## Install

1. Create the directory `/config/packages/` in Home Assistant if it does not exist.
2. Copy `f1_race_control.yaml` to `/config/packages/f1_race_control.yaml`.
3. Enable packages in `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

4. Check the Home Assistant configuration and restart Home Assistant.
5. Confirm that these helper entities exist:
   - `sensor.f1_race_p1`
   - `sensor.f1_race_p2`
   - `sensor.f1_race_p3`
   - `sensor.f1_eliminated_1` through `sensor.f1_eliminated_6`

## Required source entities

The helper package expects at least:

- `sensor.f1_driver_positions`
- `sensor.f1_session_time_remaining`

The ESPHome firmware additionally expects the F1 entities documented in the main README, including `number.f1_live_delay`.

> The F1 data integration itself is not included in this repository.
