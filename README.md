# Het Stuyvesant Huys — mobiele web-app (PWA)

Sfeervolle mobiele web-app voor gastenverblijf **Het Stuyvesant Huys** in Wolvega, Friesland.
Pagina's: Home · Verblijf · Omgeving · Informatie · Contact, plus een boekingsflow in vier stappen.

## Bestanden

| Bestand | Doel |
|---|---|
| `index.html` | De volledige app (HTML, CSS en JavaScript in één bestand) |
| `manifest.webmanifest` | PWA-manifest (naam, kleuren, iconen, standalone-weergave) |
| `sw.js` | Service worker — offline gebruik en snel herladen |
| `icon.svg` | Schaalbaar app-icoon (H·S-schild) |
| `icon-192.png`, `icon-512.png` | App-iconen (Android / installatie) |
| `apple-touch-icon.png` | App-icoon voor iOS ("Zet op beginscherm") |
| `favicon-32.png` | Browser-tabicoon |

## Publiceren op je `.app`-domein

1. Zet **alle** bestanden samen in de hoofdmap van je hosting (bijv. Netlify, Vercel, Cloudflare Pages, GitHub Pages of eigen webruimte).
2. Zorg dat de site via **HTTPS** wordt geserveerd (verplicht voor een PWA en voor een `.app`-domein).
3. Koppel je `.app`-domein aan de hosting.

Daarna kunnen bezoekers de site niet alleen bekijken, maar ook **installeren** ("Zet op beginscherm" / "App installeren") met een eigen icoon, splash-kleuren en offline-ondersteuning.

> Let op: PWA-functies (installeren, offline, service worker) werken alleen op de échte, via HTTPS geserveerde site — niet in een losse voorbeeldweergave.

## Zelf inhoud aanpassen (in `index.html`)

- **Prijs & kosten** — zoek naar `const PRICE=` (prijs per nacht, schoonmaak- en servicekosten).
- **Max. aantal gasten** — zoek naar `MAX_GUESTS`.
- **Contactgegevens** — zoek naar `views.contact` (adres, telefoon, e-mail, website).
- **Social media links** — zoek naar `instagram.com` / `facebook.com` en vul je eigen profiel-URL's in.
- **Omgeving-teksten** — zoek naar `const AREA=`.
- **Kamers (Verblijf)** — zoek naar `const STAY=`.
- **Informatie & FAQ** — zoek naar `const INFO=` en `const FAQ=`.
- **Foto's** — de sfeerbeelden zijn nu stijlvolle kleur-placeholders; deze worden later vervangen door echte foto's.

## Boeken

Boeken werkt nu als **aanvraag**: bij "Boek verblijf" opent het mailprogramma met alle gegevens klaar voor `info@stuyvesanthuys.nl`. Voor écht online boeken met beschikbaarheid en betaling kan later een boekingssysteem worden gekoppeld.

## Een nieuwe versie uitrollen

Pas `index.html` aan en verhoog in `sw.js` de regel `const CACHE = 'hsh-v1'` (bijv. naar `hsh-v2`), zodat bezoekers de nieuwe versie zeker binnenkrijgen.
