# Hardware

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

## English

### Tested controller

Waveshare ESP32-S3 RGB Matrix, ESP32-S3-N32R16 (32 MB flash / 16 MB PSRAM).

### Tested panel

128×64 HUB75E RGB matrix, P2.5, 320×160 mm, 1/32 scan. The tested panel uses an ICND2153-family driver.

### HUB75 pin mapping

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

The validated generic ESPHome HUB75 timing uses 20 MHz, clock phase enabled, latch blanking 8, bit depth 4 and double buffering.

### Power

Use a regulated 5 V supply with sufficient current for your panel and controller. The development unit uses a 5.1 V / 5 A USB-C supply. Size the supply for your own panel specification and brightness.

---

<a id="nederlands"></a>

## Nederlands

### Geteste controller

Waveshare ESP32-S3 RGB Matrix, ESP32-S3-N32R16 (32 MB flash / 16 MB PSRAM).

### Getest paneel

128×64 HUB75E RGB-matrix, P2.5, 320×160 mm, 1/32 scan. Het geteste paneel gebruikt een driver uit de ICND2153-familie.

### HUB75-pintoewijzing

| Signaal | GPIO |
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

De gevalideerde generieke ESPHome HUB75-instellingen gebruiken 20 MHz, clock phase ingeschakeld, latch blanking 8, bit depth 4 en double buffering.

### Voeding

Gebruik een gestabiliseerde 5V-voeding met voldoende stroomcapaciteit voor je paneel en controller. De ontwikkelopstelling gebruikt een 5,1V/5A USB-C-voeding. Dimensioneer de voeding op basis van de specificaties en helderheid van je eigen paneel.
