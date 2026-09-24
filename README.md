# Vecāķu prospekts 205 — investīciju projekta mājas lapa (prototips)

Viena faila (single-page) landing lapa **attīstības/investīciju projekta pārdošanai vienam
investoram vai attīstītājam**. LV / EN / RU. Statisks HTML — bez build soļa, bez backend.
Deploy uz GitHub Pages vai jebkuru hostingu.

**`index.html` ir pilnībā pašpietiekams** — visi attēli iešūti failā kā base64 (nevis saites
uz `assets/`), tāpēc tas droši jāsūta/jākopē kā **viens fails** bez riska, ka bildes pazūd.
`assets/` mape ir tikai avota/rezerves oriģināli, ko izmantot, ja attēli jāpiemaina (skat. zemāk).

## Sadaļas
Hero (investīciju iespēja) → **Finanses** (CAPEX/NOI/Cap Rate/atmaksāšanās + budžeta un
ieņēmumu sadalījums) → Iespēja (4 pārdošanas argumenti) → Atrašanās vieta (karte, mājas
piktogramma) → Arhitektūra (gatavs tehniskais projekts) → Skaitļos (darījuma dati, 10 rādītāji,
t.sk. 32 dzīvokļi) → Korpusi A/B/C/D (fāzēta attīstība, 8 dzīvokļi katrā) → **Investīciju
struktūra** (2 scenāriji: Kreditors / Investors) → **Realizācijas grafiks** (18–24 mēneši) →
Investīciju memoranda pieprasījums.

## Struktūra
```
index.html                # galvenā lapa (HTML + CSS + JS + i18n) — attēli iešūti base64
privatuma-politika.html   # privātuma politika (LV/EN/RU, GDPR)
assets/
  hero.jpg          # avota fails — kvartāls priedēs (iešūts index.html)
  render-1.jpg      # avota fails — koka fasādes tuvplāns (iešūts)
  render-2.jpg      # avota fails — iekšpagalma panorāma (iešūts)
  satellite.jpg     # satelīta skats ar atrašanās vietu (rezervē, nav izmantots)
```

## Ja jāmaina attēli
1. Aizvieto failu `assets/hero.jpg` (vai citu) ar jauno versiju — **saglabā to pašu nosaukumu**.
2. Atkārtoti iešuj to `index.html` (aizstāj veco base64 versiju ar jauno):
```bash
cd Vecaku-205-website
python3 -c "
import base64, pathlib
p = pathlib.Path('index.html'); html = p.read_text(encoding='utf-8')
import re
# atrod esošo šī attēla base64 URI un aizstāj ar jaunu no assets/<name>
"
```
   (Vienkāršāk: prasi Claude vēlreiz iešūt attēlus — tas ir ātrs, atkārtojams solis.)

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

## Kas jāaizpilda pirms publicēšanas (placeholder → īstie dati)
- **Tālrunis / e-pasts** — `index.html`, sadaļā `.contact-info` (+371 20 000 000, info@vecaku205.lv)
- **Pieteikuma forma** — `<form action="https://formspree.io/f/your-id">` → ieliec īsto Formspree ID
  (vai pieslēdz citu servisu). Kamēr `your-id`, forma tikai parāda paziņojumu, nesūta.
- **Privātuma politika** — `privatuma-politika.html` sadaļā “1. Pārzinis” aizpildi
  `[Uzņēmuma nosaukums, reģistrācijas Nr., juridiskā adrese]`.
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
