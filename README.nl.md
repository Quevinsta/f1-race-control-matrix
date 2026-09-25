# F1 Race Control Matrix

Een onofficieel communityproject voor een 128×64 HUB75-ledmatrix, aangestuurd door ESPHome en Home Assistant.

Het project verandert een Waveshare ESP32-S3 RGB Matrix-controller en HUB75-paneel in een compact Race Control- en live-timingdisplay met sessielabels, top-3 timing, racegaten, rondeteller, baanstatusanimaties, kwalificatie-eliminatieschermen en instelbare F1TV/Viaplay-synchronisatie.

> **Status:** private ontwikkelversie. De huidige configuratie wordt vanuit de geteste V12.6.37-firmware opgeschoond voordat de repository openbaar wordt gemaakt.

[English README](README.md)

## Hardware

- Waveshare ESP32-S3 RGB Matrix-board (ESP32-S3-N32R16)
- 128×64 HUB75/HUB75E RGB-matrix
- Getest paneel: P2.5, 320×160 mm, 1/32 scan
- 5V-voeding met voldoende stroomcapaciteit
- Home Assistant
- ESPHome 2026.9.0

## Functies

- F1 Race Control / live-timingpagina
- Ondersteuning voor vrije trainingen, kwalificatie, sprintkwalificatie, sprint en race
- Q1/Q2/Q3-sessielabels
- Top-3 timing en racegaten
- Huidige/totale rondeweergave voor race en sprint
- GREEN-, YELLOW-, RED-, VSC-, SC- en CHEQUERED-animaties
- Timingpagina blijft 10 minuten zichtbaar nadat een sessie is afgelopen
- Race Control-standbyscherm buiten sessies
- F1TV/Viaplay-synchronisatie
- Kwalificatie-eliminatiescherm (experimenteel)
- Automatisch omschakelen naar Race Control kort voor een sessie

## Indeling van de repository

- `esphome/` — ESPHome-firmware en voorbeeld-secrets
- `home-assistant/` — templatesensoren en automatiseringen
- `docs/` — hardware-, installatie- en entiteitdocumentatie
- `CHANGELOG.md` — wijzigingen aan het project

## Belangrijk

Dit is een onofficieel project en is niet verbonden aan, goedgekeurd door of gelieerd aan Formula 1, de FIA, Formula One Management of een omroep/streamingdienst.

Deze repository bevat geen officiële Formula 1-logo's of auteursrechtelijk beschermde broadcastgraphics. Gebruikers zijn zelf verantwoordelijk voor de databron/integratie die zij met Home Assistant verbinden en voor naleving van de bijbehorende voorwaarden en toepasselijke rechten.

## Huidige ontwikkelbasis

De eerste GitHub-versie is gebaseerd op de lokaal geteste **V12.6.37**-configuratie. Persoonlijke inloggegevens, lokale netwerkgegevens en huishoudspecifieke configuratie worden verwijderd voordat het project openbaar wordt gemaakt.

## Licentie

MIT. Zie `LICENSE`.
