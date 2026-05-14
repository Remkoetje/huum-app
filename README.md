# HUUM Sauna App — Projectsamenvatting

## Wat we gebouwd hebben
Een webapp om een HUUM sauna te bedienen via de HUUM cloud API, inclusief lichtschema's op basis van vaste tijden of zonsopgang/zonsondergang.

## Architectuur
```
Webapp (GitHub Pages)
        ↓
Proxy (Railway)
        ↓
api.huum.eu (HUUM cloud)
        ↓
Sauna 🧖
```

## Bestanden en locaties

### Proxy (Node.js)
- **GitHub repo:** `huum-proxy` (privé)
- **Live URL:** `https://huum-proxy-production.up.railway.app`
- **Platform:** Railway ($5/maand Hobby-plan)
- **Functie:** Lost CORS op, stuurt commando's naar HUUM API, voert lichtschema's 24/7 uit

### Webapp
- **GitHub repo:** `huum-app` (publiek)
- **Live URL:** `https://[gebruikersnaam].github.io/huum-app`
- **Platform:** GitHub Pages (gratis)
- **Functie:** UI voor bediening sauna en instellen schema's

## HUUM API endpoints (via proxy)
| Methode | Endpoint | Functie |
|---|---|---|
| GET | `/status` | Saunastatus ophalen |
| POST | `/start` | Sauna aanzetten |
| POST | `/stop` | Sauna uitzetten |
| GET/POST | `/light` | Licht toggling (1 endpoint, schakelt steeds om) |
| POST | `/schedules` | Schema's opslaan op Railway (24/7) |
| GET | `/schedules` | Schema's ophalen |
| GET | `/suntimes` | Zonsopgang/ondergang berekenen |

## Authenticatie
- HUUM email + wachtwoord via Basic Auth
- Opgeslagen in localStorage van de browser
- Automatisch inloggen bij pagina-reload

## Lichtschema's
- Instelling: vaste tijd (per 15 min) of zonsopgang/zonsondergang + offset
- Dagen selecteerbaar (Ma t/m Zo)
- Schema's opgeslagen op Railway, draaien 24/7
- ⚠️ Na Railway-herstart opnieuw opslaan via "Opslaan op server"-knop

## Locatie
- Vaste coördinaten Almere (52.3851, 5.1954)
- Geen locatiepermissie nodig

## Bekende beperkingen
- Licht heeft geen aan/uit-status — HUUM API heeft maar 1 toggle-endpoint
- Schema's gaan verloren bij Railway-herstart (nog geen database)
- Schema's overleven herstart niet — volgende stap: opslaan in bestand/database

## Volgende mogelijke stappen
1. Schema's persistent maken (bijv. met een JSON-bestand of kleine database op Railway)
2. PWA instellen zodat app installeerbaar is op homescreen Android
3. Beveiliging toevoegen zodat anderen de proxy niet kunnen gebruiken
4. Sauna ook in schema's opnemen (niet alleen licht)
