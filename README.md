# ’t Stuyvesant Huys — mobiele web-app (PWA)

Sfeervolle mobiele web-app voor gastenverblijf **’t Stuyvesant Huys** in Wolvega, Friesland.
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
| `og-image.png` | Deel-afbeelding (1200×630) voor WhatsApp / social / Google |

## Publiceren op je `.app`-domein

1. Zet **alle** bestanden samen in de hoofdmap van je hosting (bijv. Netlify, Vercel, Cloudflare Pages, GitHub Pages of eigen webruimte).
2. Zorg dat de site via **HTTPS** wordt geserveerd (verplicht voor een PWA en voor een `.app`-domein).
3. Koppel je `.app`-domein aan de hosting.

Daarna kunnen bezoekers de site niet alleen bekijken, maar ook **installeren** ("Zet op beginscherm" / "App installeren") met een eigen icoon, splash-kleuren en offline-ondersteuning.

> Let op: PWA-functies (installeren, offline, service worker) werken alleen op de échte, via HTTPS geserveerde site — niet in een losse voorbeeldweergave.

**Belangrijk voor delen & Google:** vervang bovenin `index.html` de voorbeelddomeinnaam `https://stuyvesanthuys.app` (in de `og:`-tags, `canonical` en de `application/ld+json`-blok) door je échte `.app`-domein. Zo tonen WhatsApp/social een nette voorbeeldkaart en herkent Google je adres. Pas in dat `ld+json`-blok ook het telefoonnummer aan als het definitief is.

## Zelf inhoud aanpassen

**Zonder code — via het beheerscherm** (zie hieronder): tarieven, **seizoensprijzen, weekendtoeslag en minimum verblijf**, max. aantal gasten, contactgegevens (incl. **WhatsApp**), de **agenda-koppeling** (iCal), social-links én de teksten van de huisregels en annuleringsvoorwaarden.

**In `index.html`** (voor de overige inhoud):
- **Standaard-instellingen** — zoek naar `const DEFAULTS=` (prijs, kosten, max. gasten, contact, social, en de standaardteksten van de voorwaarden). Het beheerscherm bewerkt deze waarden; de code houdt de standaard aan.
- **Omgeving-teksten** — zoek naar `const AREA=`.
- **Kamers (Verblijf)** — zoek naar `const STAY=`.
- **Informatie & FAQ** — zoek naar `const INFO=` en `const FAQ=`.
- **Foto's** — de sfeerbeelden zijn nu stijlvolle kleur-placeholders; deze worden later vervangen door echte foto's.

## Talen (NL / EN / DE)

De app is drietalig: **Nederlands, Engels en Duits**. Bezoekers wisselen van taal via de **taalkiezer in het menu** (hamburger linksboven → NL · EN · DE). De keuze wordt onthouden op het apparaat, en bij een eerste bezoek kiest de app automatisch de browsertaal (met Nederlands als standaard).

Vertalingen aanpassen in `index.html`:
- **Losse teksten en knoppen** — het object `const TR=` (elke tekst heeft `nl`, `en` en `de`).
- **Pagina-inhoud** (kamers, omgeving, informatie, FAQ, huisinstructies) — de data-arrays `STAY`, `AREA`, `INFO`, `FAQ` en `HOUSE`, waar elk tekstveld ook `nl` / `en` / `de` bevat.

## Beheerscherm & statistieken

Open het **beheerscherm** door **5× op het H·S-embleem** bovenaan te tikken, of ga op je eigen domein naar `.../#beheer`. Het is beveiligd met een **pincode** (standaard `1592` — wijzig deze in het scherm).

- **Instellingen** — contactgegevens (telefoon, **WhatsApp-nummer**, e-mail, website, adres), de **agenda-koppeling** (iCal, zie hieronder), max. aantal gasten en social-links. "Opslaan" geldt meteen op dít apparaat; met **Download settings.json** krijg je een klein bestand dat je in de hoofdmap van je hosting zet om de wijziging voor álle gasten live te maken (of kopieer de getoonde inhoud).
- **Prijzen** — basistarief per nacht, **weekendtoeslag** (vr/za), schoonmaak- en servicekosten, **minimum aantal nachten**, en **seizoensprijzen**: per periode (datums als `MM-DD`, mag over de jaarwisseling lopen) een eigen nachtprijs en optioneel minimum verblijf.
- **Voorwaarden** — bewerk de teksten van de **huisregels** en **annuleringsvoorwaarden** per taal (NL / EN / DE). Begin een regel met `-` voor een opsommingspunt en met `>` voor een cursieve slotregel; een lege regel begint een nieuwe alinea. Ook deze teksten komen mee in **settings.json** voor alle gasten.
- **Statistieken** — privacyvriendelijk en cookieloos: paginaweergaven, taalkeuze, boekingsverloop en contactberichten. De cijfers worden alleen op dít apparaat bijgehouden (ideaal voor bijv. een vaste huis-tablet). Voor cijfers over álle bezoekers kan later een privacy-vriendelijke dienst (Plausible/GoatCounter) worden gekoppeld.

Als `settings.json` op de hosting staat, overschrijft dat de standaardwaarden; instellingen die je op je eigen apparaat opslaat, winnen tijdens het bewerken.

## Beschikbaarheid — bezette datums blokkeren (Airbnb / iCal)

In het beheerscherm (tab **Instellingen → Beschikbaarheid**) kun je één of meer **iCal-links** invullen (één per regel). Bezette datums uit die agenda's worden in de boekingskalender **doorgestreept en geblokkeerd**, en gasten kunnen geen periode kiezen die over een bezette nacht loopt.

> **Let op — Airbnb en CORS:** een browser mag de iCal-link van Airbnb zelf meestal niet rechtstreeks ophalen (CORS-blokkade). Zet daarom bij voorkeur een **`calendar.ics` op je eigen domein** die met Airbnb synchroniseert (veel hostingpartijen of een klein Cloudflare Worker-scriptje kunnen de Airbnb-feed periodiek ophalen en cachen), en vul die eigen `calendar.ics`-URL hier in. Een link op je eigen domein werkt altijd. Lukt het ophalen niet, dan blijft de app gewoon werken — er worden dan alleen geen datums geblokkeerd.

## WhatsApp & kaart

- **WhatsApp** — vul je WhatsApp-nummer in bij Instellingen. Er verschijnt dan een WhatsApp-knop op de **Contact**-pagina, in het **menu** en in de **huismap**, met een vooringevuld bericht.
- **Kaart** — het kaartje op Home en het adres op Contact zijn klikbaar en openen **Google Maps** met het adres gepind. De pin volgt het adres uit het beheerscherm.

## Digitale huismap (voor gasten)

Een aparte gastenpagina met **huisinstructies** (WiFi, verwarming, tv, koffie, afval, badkamer, e-bike, check-out) plus een snelle hulp-knop (bellen / WhatsApp). Bereikbaar via het **menu** of rechtstreeks via `.../#huismap` — handig om als **QR-code** in huis op te hangen. De onderwerpen bewerk je in `index.html` bij `const HOUSE=`.

## Delen & vindbaarheid (SEO)

- **Deel-preview** — deel je de link (WhatsApp, social), dan verschijnt een nette voorbeeldkaart met titel, omschrijving en `og-image.png`.
- **Google** — er staat `LodgingBusiness`-structuurdata (schema.org) in de pagina met naam, adres en voorzieningen.
- Vergeet niet het voorbeelddomein `stuyvesanthuys.app` bovenin `index.html` te vervangen door je échte domein (zie *Publiceren*).

## Toegankelijkheid

De app is nagelopen op toegankelijkheid: tekstkleuren voldoen aan het **WCAG AA-contrast**, alle knoppen hebben een zichtbare focus en een label, de overlays (menu, documenten, beheer) zijn als dialoog gemarkeerd en sluiten met **Esc**, en bezette kalenderdagen worden ook voor schermlezers als "bezet" aangekondigd.

## Boeken

Boeken werkt nu als **aanvraag**: bij "Boek verblijf" opent het mailprogramma met alle gegevens klaar voor `info@stuyvesanthuys.nl`. Voor écht online boeken met beschikbaarheid en betaling kan later een boekingssysteem worden gekoppeld.

## Een nieuwe versie uitrollen

Pas `index.html` aan en verhoog in `sw.js` de regel `const CACHE = 'hsh-v5'` (bijv. naar `hsh-v6`), zodat bezoekers de nieuwe versie zeker binnenkrijgen.
