# Installatie

> 🇳🇱 Nederlandse installatiehandleiding. Voor de Engelse versie: [INSTALLATION.md](INSTALLATION.md).

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
2. Plaats het Waveshare ESP32-S3 RGB Matrix-board **rechtstreeks op de HUB75/HUB75E INPUT-connector van het LED-paneel**. Er is dus geen HUB75-lintkabel nodig tussen het Waveshare-board en het paneel.
3. Controleer de richting van de connector en zorg dat het board op de **INPUT** van het paneel zit, niet op de uitgang.
4. Sluit de USB-C-voedingsadapter aan op de speciale **POWER** USB-C-aansluiting van het Waveshare-board. **Sluit de voedingsadapter niet aan op de USB-aansluiting die voor data/programmeren wordt gebruikt.**
5. Voor de geteste opstelling levert een Raspberry Pi 5 27 W USB-C-adapter voldoende vermogen.

Sluit de HUB75-kabel niet aan of af terwijl de opstelling onder spanning staat.

### 2. Home Assistant voorbereiden

Installeer eerst de **F1 Sensor** custom integration van Nicxe:

**https://github.com/Nicxe/f1_sensor**

Dit project gebruikt deze integratie als F1-databron. Voeg de repository via **HACS** als custom repository toe aan Home Assistant, installeer de integratie, herstart Home Assistant wanneer daarom wordt gevraagd en configureer daarna F1 Sensor voordat je verdergaat met deze handleiding.

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