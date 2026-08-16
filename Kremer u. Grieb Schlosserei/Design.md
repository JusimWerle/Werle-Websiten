# DESIGN.md – Kremer u. Grieb Schlosserei

## 1. Konzept & Vibe
- **Produkt:** Einseitige Website für Schlosserei & Metallbau „Kremer u. Grieb Schlosserei" in Altrip.
- **Zielgruppe:** Privat- und Gewerbekunden in Altrip/Rhein-Pfalz-Kreis, die Metall-/Schlosserarbeiten (Zaun, Tor, Geländer, Treppen, Carport, Sicherheitstechnik) benötigen.
- **Primärziel:** Anrufe zur Angebotsanfrage.
- **Vibe (3–5 Adjektive):** solide, vertrauenswürdig, präzise, robust, klar.
- **Tonalität der Texte:** sachlich, direkt, unaufgeregt — Handwerker-Ton ohne Marketing-Floskeln.

## 2. Farbsystem (semantische Tokens → Hex)
| Token | Hex | Verwendung |
|-------|-----|------------|
| `--color-primary` | #1E293B | Hauptmarkenfarbe (Anthrazit), Header, Hero-Hintergrund, primäre Flächen |
| `--color-primary-hover` | #0F172A | Hover/Active auf Primärflächen |
| `--color-accent` | #EA580C | Signalorange — CTA-Buttons, Icons, Hervorhebungen |
| `--color-accent-hover` | #C2410C | Hover/Active auf Akzent-Buttons |
| `--color-bg` | #F8FAFC | Seitenhintergrund |
| `--color-surface` | #FFFFFF | Karten/Sektionsflächen |
| `--color-on-surface` | #334155 | Fließtext auf Surface (Kontrast ≥ 4.5:1 auf #FFFFFF) |
| `--color-on-primary` | #F8FAFC | Text auf `--color-primary` (Kontrast ≥ 4.5:1 auf #1E293B) |
| `--color-muted` | #64748B | Sekundärtext (Kontrast ≥ 3:1) |
| `--color-border` | #E2E8F0 | Linien/Trenner/Kartenrahmen |
| `--color-danger` | #DC2626 | Platzhalter-/Warnhinweise (z.B. „bitte bestätigen") |

- **Dark Mode:** nein. Einfacher, robuster Ein-Modus-Auftritt für einen lokalen Handwerksbetrieb.

## 3. Typografie
- **Heading-Font:** Lexend (Google Fonts), Gewichte 600 (Semibold) / 700 (Bold)
- **Body-Font:** Source Sans 3 (Google Fonts), Gewichte 400 (Regular) / 600 (Semibold für Hervorhebungen)
- **Type-Scale (px):** H1 44 / H2 32 / H3 22 / Body 16 / Small 14
- **Line-height:** Headings 1.15–1.25 / Body 1.6
- **Regeln:** Body ≥ 16px, Zeilenlänge 60–75 Zeichen im Fließtext, Gewichte statt Farbschwankungen zur Hierarchie nutzen.

## 4. Spacing & Layout
- **Base unit:** 8px. **Scale:** 4, 8, 12, 16, 24, 32, 48, 64, 96px.
- **Container max-width:** 1152px (max-w-6xl), seitliche Gutter mobil 20px.
- **Grid:** Leistungskarten 3-spaltig Desktop (≥1024px) / 2-spaltig Tablet (≥768px) / 1-spaltig Mobil.
- **Breakpoints:** 375 / 768 / 1024 / 1440.

## 5. Form & Effekte
- **Border-Radius:** sm 4px / md 8px / lg 12px / full (Pills nur für Badges).
- **Schatten:** card `0 1px 3px rgba(15,23,42,.08), 0 1px 2px rgba(15,23,42,.06)`; elevated (Hover) `0 4px 12px rgba(15,23,42,.12)`.
- **Icons:** eine SVG-Icon-Familie (Heroicons, outline), keine Emojis als Icons. Je Leistungskarte ein passendes Icon (Zaun, Tor, Treppe, Schweißen/Funke, Schutzschild, Carport, Gitter, Briefkasten).
- **Motion:** Micro-Interaktionen 150–250ms ease-out (Hover auf Karten/Buttons: leichte Anhebung + Schattenwechsel), `prefers-reduced-motion` respektieren (Transitions dann deaktivieren).

## 6. Komponenten (Kurz-Spezifikation)
- **Button (primär/Accent):** Fläche `--color-accent`, Text weiß, Radius md, Padding 14px/28px, Hover `--color-accent-hover`, sichtbarer Fokus-Ring (2px, `--color-accent`, Offset 2px).
- **Button (sekundär):** Outline 1.5px `--color-border` auf `--color-primary`-Flächen in Weiß/Transparent, Text `--color-on-primary`, Hover leichte weiße Füllung 10%.
- **Card (Leistung):** `--color-surface`, Border 1px `--color-border`, Radius lg, Padding 24px, Icon 40px in `--color-accent`, Titel H3, Kurztext `--color-muted`.
- **Nav:** sticky Header, halbtransparent bei Scroll, links Wortmarke „Kremer u. Grieb Schlosserei", rechts Anker-Links (Leistungen, Über uns, Kontakt) + Telefon-Button (Accent) durchgängig sichtbar.
- **Kontaktblock:** Adresse/Telefon in großer, gut lesbarer Schrift, Klick-zum-Anrufen (`tel:`-Link) mit Icon.
- **Platzhalter-Badge:** kleines Label in `--color-danger`/hellorange Hintergrund für alle offenen Punkte (z.B. „Öffnungszeiten bitte bestätigen"), klar als Hinweis für den Inhaber erkennbar, nicht als echte Kundeninformation getarnt.

## 7. Layout pro Sektion (Zoom-In-Prompts)
- **Header:** Sticky-Bar, Hintergrund `--color-primary`: links Wortmarke „Kremer u. Grieb Schlosserei" (weiß), mittig/rechts Anker-Links (Leistungen, Über uns, Kontakt) in `--color-on-primary`, ganz rechts Telefon-CTA-Button (Accent). Mobil: Hamburger-Menü, Telefon-Icon bleibt sichtbar.
- **Hero:** Vollbreite auf `--color-primary`-Hintergrund mit dezenter abstrakter Linien-/Metallstruktur (SVG-Pattern, kein Stockfoto). Zweispaltig Desktop: links H1 „Schlosserei & Metallbau in Altrip — seit 1997" + Subline (kurze Leistungszusammenfassung) + zwei CTAs („Jetzt anrufen" Accent-Button, „Anfahrt" Outline-Button); rechts große SVG-Illustration/Icon-Komposition (Zaun/Tor-Motiv). Einspaltig mobil, CTAs untereinander volle Breite.
- **Leistungen:** Überschrift „Unsere Leistungen" + Subline. 3-Spalten-Kartengrid Desktop (2 Tablet, 1 Mobil) mit Icon, Titel, Kurztext pro Leistung (Zäune, Tore, Geländer, Garagentore/-antriebe, Briefkastenanlagen, Hausabsicherung, Stahltreppen, Carports/Überdachungen, Fenstergitter, Edelstahlverarbeitung, allgemeine Schlosser-/Schweißarbeiten).
- **Über uns:** Einspaltig, max-width ~720px zentriert oder zweispaltig mit Kennzahlen-Leiste („seit 1997", „Schlosserei & Metallbau", „Altrip & Umgebung") neben kurzem Fließtext zur Betriebsgeschichte (nur belegte Fakten).
- **Öffnungszeiten:** Kompakte Sektion/Card auf `--color-surface`, Platzhalter-Badge „Öffnungszeiten bitte bestätigen", Hinweis „Bitte vorab anrufen" mit Telefon-CTA.
- **Kontakt & Anfahrt:** Zweispaltig Desktop: links Adresse (Reginostr. 6, 67122 Altrip), Telefon (groß, klickbar), Platzhalter für E-Mail; rechts eingebettete Google-Maps-Karte (statisches iframe-Embed ohne API-Key, `q=Reginostr.+6,+67122+Altrip`). Einspaltig mobil, Karte unter den Kontaktdaten.
- **Footer:** Dunkler Streifen (`--color-primary`), Kontaktzeile (Adresse/Telefon) + Copyright „© 2026 Kremer u. Grieb Schlosserei" + Links zu Impressum/Datenschutz (Platzhalter-Seiten).

## 8. Barrierefreiheit & Qualität (Pflicht)
- Kontraste AA (Text ≥ 4.5:1): `--color-on-surface` auf `--color-surface`/`--color-bg`, `--color-on-primary` auf `--color-primary`, Accent-Button-Text weiß auf `#EA580C` geprüft.
- Sichtbare Fokuszustände auf allen interaktiven Elementen (Buttons, Links, Anker-Nav).
- Alt-Texte für alle SVG-Icons/Illustrationen (aria-label oder alt), semantisches HTML (header/nav/main/section/footer, korrekte Heading-Hierarchie h1→h3).
- Touch-Ziele ≥ 44px (Buttons, Nav-Links), kein horizontales Scrollen auf Mobil, `viewport`-Meta gesetzt.
- Siehe Quick Reference §1–§10 in `references/ui-ux-pro-max.md`.
