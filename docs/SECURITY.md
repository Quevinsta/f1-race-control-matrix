# Security / Beveiliging

<p align="center">
  <strong>🇬🇧 English</strong> &nbsp;|&nbsp; <a href="#nederlands">🇳🇱 Nederlands</a>
</p>

## English

The public firmware uses encrypted ESPHome API communication and encrypted OTA updates.

### Required local secrets

Keep these values only in your local `secrets.yaml`:

- `wifi_ssid`
- `wifi_password`
- `api_encryption_key`

Generate a unique API key for every controller:

```bash
openssl rand -base64 32
```

OTA uses ESPHome's encrypted OTA transport as configured by the firmware. No separate OTA secret is referenced by this configuration.

Never commit your real `secrets.yaml`. If a key or password is accidentally published, rotate it before continuing to use the device.

---

<a id="nederlands"></a>

## Nederlands

De publieke firmware gebruikt versleutelde ESPHome API-communicatie en versleutelde OTA-updates.

### Vereiste lokale secrets

Bewaar deze waarden uitsluitend in je lokale `secrets.yaml`:

- `wifi_ssid`
- `wifi_password`
- `api_encryption_key`

Genereer voor iedere controller een unieke API-sleutel:

```bash
openssl rand -base64 32
```

OTA gebruikt het versleutelde OTA-transport van ESPHome zoals dit in de firmware is geconfigureerd. Deze configuratie verwijst niet naar een aparte OTA-secret.

Commit je echte `secrets.yaml` nooit naar Git. Als een sleutel of wachtwoord per ongeluk openbaar is gemaakt, vervang die dan voordat je het apparaat verder gebruikt.
