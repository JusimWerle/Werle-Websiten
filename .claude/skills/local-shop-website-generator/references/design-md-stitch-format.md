# Referenz: `Design.md` im Google-Stitch-Format

Ziel: `design-anforderungen.md` in eine `Design.md` übersetzen, die dem **Google-Stitch-`DESIGN.md`-
Format** entspricht. Kernidee von Stitch: `DESIGN.md` ist eine **portable Markdown-Datei, die das
komplette Design-System als Konstanten kodiert** — Farben mit semantischen Tokens, Typografie, Spacing,
Radius/Schatten, Komponenten — plus knappe, screen-/sektionsweise Layout-Prompts. Das Modell behandelt
diese Werte beim Bauen als **harte Vorgaben, nicht als Vorschläge**. Genau so nutzen wir sie in Schritt 7.

## Was das Format ausmacht
- **Semantische Tokens statt roher Hex im Markup:** `primary`, `surface`, `accent`, `on-surface` …
  jeweils mit konkretem Hex-Wert an **einer** Stelle definiert.
- **Vollständige, aber knappe Systemtabellen** für Farbe, Typografie, Spacing, Radius, Schatten.
- **Konzept + Vibe zuerst:** ein „Zoom-Out"-Kontext (Was ist das Produkt, für wen), dann pro Sektion
  ein „Zoom-In" mit Layout-Hierarchie.
- **Maschinen- und menschenlesbar:** klare Überschriften, Tabellen, kurze Bullet-Prompts.
- **Konkret statt vage:** nicht „modern", sondern „vier-Spalten-Grid, auf Tablet zwei, auf Mobil eins".

## `Design.md` — vollständiges Template
Fülle alles mit den echten Entscheidungen aus `design-anforderungen.md` und der Marke aus `Daten.md`.
(Vorlage auch unter `templates/Design.template.md`.)

```markdown
# DESIGN.md – <Name des Shops>

## 1. Konzept & Vibe
- **Produkt:** Einseitige Website für <Branche> „<Name>" in <Ort>.
- **Zielgruppe:** <…>
- **Primärziel:** <z.B. Anrufe / Laufkundschaft>
- **Vibe (3–5 Adjektive):** <z.B. warm, handwerklich, einladend, vertrauenswürdig>
- **Tonalität der Texte:** <z.B. herzlich, regional, unaufgeregt>

## 2. Farbsystem (semantische Tokens → Hex)
| Token | Hex | Verwendung |
|-------|-----|------------|
| `--color-primary` | #RRGGBB | Hauptmarkenfarbe, primäre CTAs |
| `--color-primary-hover` | #RRGGBB | Hover/Active der Primärfläche |
| `--color-accent` | #RRGGBB | Akzente, Highlights |
| `--color-bg` | #RRGGBB | Seitenhintergrund |
| `--color-surface` | #RRGGBB | Karten/Sektionsflächen |
| `--color-on-surface` | #RRGGBB | Fließtext auf Surface (Kontrast ≥ 4.5:1) |
| `--color-muted` | #RRGGBB | Sekundärtext (Kontrast ≥ 3:1) |
| `--color-border` | #RRGGBB | Linien/Trenner |
| `--color-success` / `--color-danger` | #RRGGBB | Status (falls nötig) |

- **Dark Mode:** <ja/nein>. Falls ja: entsättigte, hellere Tonvarianten, Kontraste separat prüfen.

## 3. Typografie
- **Heading-Font:** <Font> (<Quelle, z.B. Google Fonts>), Gewichte <…>
- **Body-Font:** <Font>, Gewichte <…>
- **Type-Scale (px):** H1 <..> / H2 <..> / H3 <..> / Body <16> / Small <14>
- **Line-height:** Headings <1.1–1.3> / Body <1.5–1.75>
- **Regeln:** Body ≥ 16px, Zeilenlänge 60–75 Zeichen, Gewichte zur Hierarchie nutzen.

## 4. Spacing & Layout
- **Base unit:** 8px. **Scale:** 4, 8, 12, 16, 24, 32, 48, 64, 96px.
- **Container max-width:** <z.B. 1152px (max-w-6xl)>, seitliche Gutter mobil <16–24px>.
- **Grid:** <z.B. 12-Spalten Desktop; Karten 3-spaltig Desktop / 2 Tablet / 1 Mobil>.
- **Breakpoints:** 375 / 768 / 1024 / 1440.

## 5. Form & Effekte
- **Border-Radius:** sm <..> / md <..> / lg <..> / full (pills).
- **Schatten:** card `0 1px 3px rgba(0,0,0,.12)`, elevated `<..>` — konsistente Skala.
- **Icons:** eine SVG-Icon-Familie (z.B. Lucide/Heroicons), keine Emojis als Icons.
- **Motion:** Micro-Interaktionen 150–300ms, ease-out beim Erscheinen, `prefers-reduced-motion` achten.

## 6. Komponenten (Kurz-Spezifikation)
- **Button (primär):** Fläche `--color-primary`, Text `--color-bg`/weiß, Radius <md>, Padding <..>,
  Hover `--color-primary-hover`, sichtbarer Fokus-Ring.
- **Button (sekundär):** Outline in `--color-border`, Text `--color-on-surface`.
- **Card:** `--color-surface`, Border/Schatten wie oben, Radius <lg>, Padding <24>.
- **Nav:** sticky, Kontakt-CTA rechts, aktueller Anker hervorgehoben.
- **Formular/Kontakt (falls vorhanden):** sichtbare Labels, Fehler unter dem Feld, Touch-Höhe ≥44px.

## 7. Layout pro Sektion (Zoom-In-Prompts)
Je Sektion ein kurzer, konkreter Layout-Prompt (Reihenfolge = Seitenaufbau):
- **Header:** <z.B. „Sticky-Bar: links Wortmarke, rechts Anker-Links + Telefon-Button.">
- **Hero:** <z.B. „Zweispaltig Desktop: links H1 + Subline + zwei CTAs, rechts großes Foto; einspaltig mobil.">
- **Leistungen/Speisekarte:** <z.B. „3-Spalten-Kartengrid mit Icon, Titel, Kurztext.">
- **Über uns:** <…>
- **Galerie:** <…>
- **Öffnungszeiten:** <…>
- **Kontakt & Anfahrt:** <z.B. „Zweispaltig: links Adresse/Telefon/Zeiten, rechts eingebettete Karte.">
- **Footer:** <z.B. „Kontaktzeile + Links zu Impressum/Datenschutz (Platzhalter).">

## 8. Barrierefreiheit & Qualität (Pflicht)
- Kontraste AA (Text ≥ 4.5:1), sichtbare Fokuszustände, Alt-Texte, semantisches HTML.
- Touch-Ziele ≥ 44px, kein horizontales Scrollen auf Mobil, `viewport`-Meta gesetzt.
- Siehe Quick Reference §1–§10 in `references/ui-ux-pro-max.md`.
```

## Qualitätskriterien für die fertige `Design.md`
- Jeder Token hat einen **konkreten Hex-Wert** (keine Lücken).
- Farbpaare erfüllen den Kontrast (nutze die Regeln aus `ui-ux-pro-max.md` §6).
- Die Sektions-Prompts sind **spezifisch** (Spaltenzahl, Responsive-Verhalten), nicht vage.
- Alles ist konsistent mit `design-anforderungen.md` und der echten Marke aus `Daten.md`.

Speichere nach `<shop>/Design.md`.
