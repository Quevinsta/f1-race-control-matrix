# Hardware

## Tested controller

Waveshare ESP32-S3 RGB Matrix, ESP32-S3-N32R16 (32 MB flash / 16 MB PSRAM).

## Tested panel

128×64 HUB75E RGB matrix, P2.5, 320×160 mm, 1/32 scan. The tested panel uses an ICND2153-family driver.

## HUB75 pin mapping

| Signal | GPIO |
|---|---:|
| R1 | 4 |
| G1 | 5 |
| B1 | 6 |
| R2 | 7 |
| G2 | 15 |
| B2 | 16 |
| A | 18 |
| B | 8 |
| C | 3 |
| D | 42 |
| E | 9 |
| CLK | 41 |
| LAT | 40 |
| OE | 2 |

The current tested generic ESPHome HUB75 timing is 20 MHz, clock phase enabled, latch blanking 8, bit depth 4 and double buffering enabled.

## Power

Use a regulated 5 V supply with enough current for your panel and controller. The development unit uses a 5.1 V / 5 A USB-C supply. Size your supply for your own panel specification and brightness.
