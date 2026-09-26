<p align="center">
  <img src="docs/images/f1-race-control-matrix-banner.png" alt="F1 Race Control Matrix — live timing en Race Control op een 128×64 HUB75 LED-matrix" width="100%">
</p>

# F1 Race Control Matrix

<p align="center">
  <a href="README.md">🇬🇧 English</a> &nbsp;|&nbsp; <strong>🇳🇱 Nederlands</strong>
</p>

Een onofficieel communityproject voor een 128×64 HUB75-ledmatrix, aangestuurd door ESPHome en Home Assistant.

Het project verandert een Waveshare ESP32-S3 RGB Matrix-controller en HUB75-paneel in een compact Race Control- en live-timingdisplay met sessielabels, top-3 timing, racegaten, rondeteller, baanstatusanimaties, kwalificatie-eliminatieschermen en instelbare F1TV/Viaplay-synchronisatie.

> **Status:** release candidate. De huidige configuratie heeft de compilevalidatie doorstaan en wordt nog tijdens live sessies getest vóór de eerste publieke release.


## Hardware

- Waveshare ESP32-S3 RGB Matrix-board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB-matrix
- Getest paneel: P2.5, 320×160 mm, 1/32 scan
- 5V-voeding met voldoende stroomcapaciteit (een Raspberry Pi 5 27 W USB-C-voedingsadapter is voldoende voor de geteste 128×64-paneelopstelling)
- Home Assistant
- ESPHome 2026.9.0

## Functies

- F1 Race Control / live-timingpagina
- Ondersteuning voor vrije trainingen, kwalificatie, sprintkwalificatie, sprint en race
- Q1/Q2/Q3-sessielabels
- Top-3 timing en racegaten (de matrix toont alleen timinggegevens van de top 3 coureurs)
- Actuele bandencompound achter iedere top-3-coureur tijdens Race en Sprint: **S** (rood), **M** (geel), **H** (wit), **I** (groen) en **W** (blauw). Hiervoor zijn de Home Assistant-templatesensoren `sensor.f1_tyre_p1`, `sensor.f1_tyre_p2` en `sensor.f1_tyre_p3` nodig.
- Huidige/totale rondeweergave voor race en sprint
- GREEN-, YELLOW-, RED-, VSC-, SC- en CHEQUERED-animaties
- Timingpagina blijft 10 minuten zichtbaar nadat een sessie is afgelopen
- Race Control-standbyscherm buiten sessies
- F1TV/Viaplay-synchronisatie
- Kwalificatie-eliminatiescherm (experimenteel)
- Automatisch omschakelen naar Race Control kort voor een sessie

## Installatie

Voor de volledige stap-voor-stap installatie — van het aansluiten van de HUB75-hardware en flashen van de controller tot Home Assistant en synchronisatie — zie de **[installatiegids](docs/INSTALLATION.nl.md)**.

## Indeling van de repository

- `esphome/` — ESPHome-firmware en voorbeeld-secrets
- `home-assistant/` — templatesensoren en automatiseringen
- `docs/` — hardware-, installatie- en entiteitdocumentatie
- `CHANGELOG.md` — wijzigingen aan het project

## Belangrijk

Dit is een onofficieel project en is niet verbonden aan, goedgekeurd door of gelieerd aan Formula 1, de FIA, Formula One Management of een omroep/streamingdienst.

Deze repository bevat geen officiële Formula 1-logo's of auteursrechtelijk beschermde broadcastgraphics. Gebruikers zijn zelf verantwoordelijk voor de databron/integratie die zij met Home Assistant verbinden en voor naleving van de bijbehorende voorwaarden en toepasselijke rechten.

## Huidige release candidate

De release candidate is gebaseerd op de geteste **V12.6.37**-ontwikkellijn en is opgeschoond voor distributie. Inloggegevens staan buiten de firmware via ESPHome-secrets. De beveiligde publieke build compileerde op 25 september 2026 succesvol met ESPHome 2026.9.0 / ESP-IDF 5.5.5.

## Licentie

MIT. Zie `LICENSE`.
