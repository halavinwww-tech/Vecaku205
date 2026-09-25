# Vecāķu prospekts 205 — investīciju projekta mājas lapa

**Dzīvs:** [vecaku205.lv](https://vecaku205.lv/) · GitHub Pages, repo
[halavinwww-tech/Vecaku205](https://github.com/halavinwww-tech/Vecaku205), zars `main`.

Viena faila (single-page) landing lapa **attīstības/investīciju projekta pārdošanai vienam
investoram vai attīstītājam**. LV / EN / RU. Statisks HTML — bez build soļa, bez backend.

**`index.html` ir pilnībā pašpietiekams** — visi attēli iešūti failā kā base64 (nevis saites
uz `assets/`), tāpēc tas droši jāsūta/jākopē kā **viens fails** bez riska, ka bildes pazūd.
`assets/` mape ir tikai avota/rezerves oriģināli, ko izmantot, ja attēli jāpiemaina (skat. zemāk).

## Sadaļas
Hero (investīciju iespēja) → **Finanses** (CAPEX/NOI/Cap Rate/atmaksāšanās + budžeta un
ieņēmumu sadalījums) → Iespēja (4 pārdošanas argumenti) → Atrašanās vieta (karte, mājas
piktogramma) → Arhitektūra (gatavs tehniskais projekts) → Skaitļos (darījuma dati, 10 rādītāji,
t.sk. 32 dzīvokļi) → Korpusi A/B/C/D (fāzēta attīstība, 8 dzīvokļi katrā) → **Investīciju
struktūra** (2 scenāriji: Kreditors / Investors) → **Realizācijas grafiks** (18–24 mēneši) →
Investīciju memoranda pieprasījums → Kājenē: tiesību piezīme (SIA "Vecāķu 205").

## Struktūra
```
index.html                # galvenā lapa (HTML + CSS + JS + i18n) — attēli iešūti base64
privatuma-politika.html   # privātuma politika (LV/EN/RU, GDPR)
CNAME                     # custom domain vecaku205.lv (GitHub Pages)
robots.txt                # crawler noteikumi + sitemap saite
sitemap.xml                # index.html + privatuma-politika.html
llms.txt                  # projekta kopsavilkums LLM/AI aģentiem (GEO)
og-cover.svg / og-cover.png  # Open Graph priekšskatījuma attēls (1200×630)
assets/
  hero.jpg          # avota fails — kvartāls priedēs (iešūts index.html)
  render-1.jpg      # avota fails — koka fasādes tuvplāns (iešūts)
  render-2.jpg      # avota fails — iekšpagalma panorāma (iešūts)
  satellite.jpg     # satelīta skats ar atrašanās vietu (rezervē, nav izmantots)
```

## SEO un GEO (AI/LLM redzamība)
- **`<head>` meta tagi** (`index.html`): description, keywords, robots, canonical,
  Open Graph (og:title/description/image/locale + LV/EN/RU alternates), Twitter Card,
  `geo.region`/`geo.placename`/`geo.position`/`ICBM`.
- **JSON-LD strukturētie dati** (2 bloki `<script type="application/ld+json">`):
  `@graph` ar `WebSite` + `Organization` (SIA "Vecāķu 205") + `ApartmentComplex`
  (32 dzīvokļi, koordinātas, adrese); atsevišķs `FAQPage` bloks ar 6 investoru jautājumiem
  (CAPEX, Cap Rate, dzīvokļu skaits, attālums līdz jūrai, investīciju scenāriji, grafiks).
- **`robots.txt`** — atļauj visiem crawleriem, norāda uz sitemap.
- **`sitemap.xml`** — 2 URL (index, privātuma politika).
- **`llms.txt`** — vienkāršs teksta kopsavilkums AI aģentiem/LLM (ChatGPT, Claude u.c.),
  kas apmeklē vietni: projekta parametri, finanšu rādītāji, investīciju struktūra,
  realizācijas grafiks, kontakti. Sekojot augošajam "GEO" (Generative Engine Optimization)
  konvencijam — sk. arī [[lipinas-energy-website]] tāda paša faila.
- **`og-cover.png`** — renderēts no `og-cover.svg` (dzīves stilā saskaņots ar lapas dizainu:
  ink/sand palete, Cormorant serifs). Rādās, koplietojot linku WhatsApp/LinkedIn/Slack u.c.

Pēc satura izmaiņām atjauno arī `og-cover.svg`/`.png` un `llms.txt`, lai tie neatpaliktu no lapas.

## Ja jāmaina attēli
1. Aizvieto failu `assets/hero.jpg` (vai citu) ar jauno versiju — **saglabā to pašu nosaukumu**.
2. Prasi Claude atkārtoti iešūt attēlus `index.html` (aizstāj veco base64 versiju ar jauno) —
   ātrs, atkārtojams solis.

## Karte
Leaflet + OpenStreetMap flīzes (bez API key). Koordinātas `lat=57.078767, lon=24.116811`
(Vecāķu prospekts 205, zoom 15), marķieris — mājas piktogramma. **Karte strādā tikai caur
serveri** (localhost/hosting) — `file://` versijā JavaScript nedarbojas, tāpēc karte un
valodu pārslēgs neparādās (bet attēli tagad rādās arī `file://`, jo ir iešūti).

## Palaišana lokāli
```bash
cd Vecaku-205-website
python3 -m http.server 8000
# atver http://localhost:8000
```

## DNS / GitHub Pages (jau iestatīts)
NIC.lv → `vecaku205.lv`: 4× A ieraksti (185.199.108-111.153), 4× AAAA ieraksti
(2606:50c0:8000-8003::153), CNAME `www` → `halavinwww-tech.github.io`. GitHub repo
Settings → Pages → Source `main`/`root`, Custom domain `vecaku205.lv`, Enforce HTTPS.

## Kas vēl jāaizpilda
- **Pieteikuma forma** — `<form action="https://formspree.io/f/your-id">` → ieliec īsto
  Formspree ID (vai pieslēdz citu servisu). Kamēr `your-id`, forma tikai parāda paziņojumu, nesūta.
- **Reģistrācijas numurs** — privātuma politikā un JSON-LD `Organization` pašlaik ir
  "SIA \"Vecāķu 205\"" bez reģ. Nr. (precizējams). Kad zināms, atjauno abviet.
- **Finanšu dati** — `index.html` sadaļā `#finance`/`#invest` skaitļi (CAPEX €6.98M, NOI €1.16M,
  Cap Rate 16.7%, atmaksāšanās 6 g., finansēšanas scenāriji A/B) ir no biznesa plāna
  (skat. Avoti). Pārbaudi/precizē pirms nosūtīšanas investoram.

## Valodas
Pārslēdzas ar LV/EN/RU pogām galvenē; izvēle saglabājas pārlūkā (localStorage).
Teksti — `index.html` objektā `I18N = { lv, en, ru }`.

## Avoti
- Vizualizācijas un fiziskie projekta dati: "Vecaku 205 concept 2021.pdf" (arhitekti BRM).
- Finanšu modelis, CAPEX/OPEX, investīciju scenāriji, realizācijas grafiks:
  "Business_Plan_Vecaku_205.pdf" (2026-09-24).
