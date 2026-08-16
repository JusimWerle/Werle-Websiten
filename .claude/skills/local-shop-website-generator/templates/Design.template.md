# DESIGN.md – <Name des Shops>

## 1. Konzept & Vibe
- **Produkt:** Einseitige Website für <Branche> „<Name>" in <Ort>.
- **Zielgruppe:** <…>
- **Primärziel:** <z.B. Anrufe / Laufkundschaft>
- **Vibe (3–5 Adjektive):** <…>
- **Tonalität der Texte:** <…>

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

- **Dark Mode:** <ja/nein>

## 3. Typografie
- **Heading-Font:** <Font>, Gewichte <…>
- **Body-Font:** <Font>, Gewichte <…>
- **Type-Scale (px):** H1 <..> / H2 <..> / H3 <..> / Body 16 / Small 14
- **Line-height:** Headings <1.1–1.3> / Body <1.5–1.75>

## 4. Spacing & Layout
- **Base unit:** 8px. **Scale:** 4, 8, 12, 16, 24, 32, 48, 64, 96px.
- **Container max-width:** <z.B. 1152px>, Gutter mobil <16–24px>.
- **Grid:** <z.B. Karten 3/2/1 Desktop/Tablet/Mobil>.
- **Breakpoints:** 375 / 768 / 1024 / 1440.

## 5. Form & Effekte
- **Border-Radius:** sm <..> / md <..> / lg <..> / full.
- **Schatten:** card `0 1px 3px rgba(0,0,0,.12)`, elevated <..>.
- **Icons:** eine SVG-Familie (Lucide/Heroicons), keine Emojis.
- **Motion:** 150–300ms, ease-out, `prefers-reduced-motion` beachten.

## 6. Komponenten
- **Button primär:** `--color-primary`, Text hell, Radius <md>, Hover `--color-primary-hover`, Fokus-Ring.
- **Button sekundär:** Outline `--color-border`, Text `--color-on-surface`.
- **Card:** `--color-surface`, Radius <lg>, Padding <24>.
- **Nav:** sticky, Kontakt-CTA rechts, aktiver Anker hervorgehoben.

## 7. Layout pro Sektion (Zoom-In-Prompts)
- **Header:** <…>
- **Hero:** <…>
- **Leistungen/Speisekarte:** <…>
- **Über uns:** <…>
- **Galerie:** <…>
- **Öffnungszeiten:** <…>
- **Kontakt & Anfahrt:** <…>
- **Footer:** <…>

## 8. Barrierefreiheit & Qualität (Pflicht)
- Kontraste AA, sichtbare Fokuszustände, Alt-Texte, semantisches HTML.
- Touch-Ziele ≥ 44px, kein horizontales Scrollen mobil, `viewport`-Meta.
- Siehe Quick Reference §1–§10 in `references/ui-ux-pro-max.md`.
