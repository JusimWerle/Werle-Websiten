# Referenz: Design-Recherche zur Nische → `design-anforderungen.md`

Ziel: herausfinden, welches Design zur **Branche/Nische** dieses Shops passt, und daraus konkrete
Design-Anforderungen ableiten — plus 2–4 Beispiel-Websites zur Orientierung. Ergebnis nach
`<shop>/design-anforderungen.md`. Diese Datei ist die Vorstufe zur `Design.md` (Schritt 5).

## Zwei Quellen kombinieren

### A) Integrierte Design-Intelligence (ui-ux-pro-max)
Nutze die eingebaute Engine für eine fundierte, branchenpassende Empfehlung. **Zwei Wege**
(siehe `references/ui-ux-pro-max.md`, Abschnitt „Prerequisites"):

- **Mit Python:** aus dem Skill-Verzeichnis
  ```bash
  python engine/scripts/search.py "<branche> <nische> <stimmung>" --design-system -p "<Shop-Name>"
  ```
  z.B. `python engine/scripts/search.py "bakery artisan cozy local" --design-system -p "Bäckerei Krönert"`.
  Optional Dials: `--variance`, `--motion`, `--density` (1–10). Liefert Pattern, Style, Farben,
  Typografie, Effekte + Anti-Patterns.
- **Ohne Python (Fallback):** lies direkt die passenden CSVs unter `engine/data/`
  (`products.csv` fürs Produkt-Muster, `styles.csv` für Stil, `colors.csv` für Paletten,
  `typography.csv` für Font-Pairings, `landing.csv` für Sektionsstruktur, `ui-reasoning.csv` für die
  Auswahllogik) und wähle passende Einträge selbst. Die Quick Reference §1–§10 in
  `references/ui-ux-pro-max.md` liefert die UX-Regeln.

### B) Reale Beispiel-Websites (Websuche)
Suche mit `WebSearch` nach Vorbildern derselben Nische, z.B.
`"best <branche> website design"`, `"<branche> website inspiration"`, `"schöne <branche> homepage"`.
Öffne 2–4 gute Beispiele (`WebFetch`) und leite ab: Farbwelt, Typografie-Gefühl, Bildsprache,
Sektionsreihenfolge, Ton. **Nichts kopieren** — nur als Orientierung für eigene, originelle Gestaltung.

## Nische → Design-Gefühl (Beispiele als Startpunkt, nicht als Dogma)
- **Bäckerei/Café:** warm, handwerklich, appetitlich; erdige/creme Töne, freundliche Serifen/rundliche Sans, viel Foto.
- **Barbier/Tattoo:** kräftig, urban, kontrastreich; dunkel + Akzentfarbe, markante Sans/Condensed.
- **Kosmetik/Spa/Nagel:** ruhig, elegant, luftig; softe Pastelle/Nude, feine Serif + leichte Sans, viel Weißraum.
- **Handwerk/Kfz:** solide, vertrauenswürdig, klar; Blau/Anthrazit + Signalakzent, robuste Sans.
- **Restaurant (gehoben):** stimmungsvoll, reduziert; dunkle Töne, elegante Serif, große Food-Fotos.
- **Blumen/Deko:** frisch, natürlich, verspielt; botanische Grün-/Rosétöne, organische Formen.

Wähle das Gefühl anhand der echten Marke aus `Daten.md` (erkennbare Logofarben, vorhandene Fotos,
Preisniveau, Ton der Rezensionen), nicht nur nach dem Klischee.

## `design-anforderungen.md` — Template
(Vorlage auch unter `templates/design-anforderungen.template.md`)

```markdown
# Design-Anforderungen – <Name des Shops>

## Nische & Design-Gefühl
- Branche/Nische: <…>
- Gewünschte Wirkung (3–5 Adjektive): <z.B. warm, handwerklich, vertrauenswürdig>

## Empfehlung aus ui-ux-pro-max
- Pattern/Produkt-Muster: <…>
- Style: <…>
- Anti-Patterns (vermeiden): <…>

## Farbwelt
- Primär / Sekundär / Akzent / Neutral(e) / Hintergrund — je mit Begründung aus Marke/Nische

## Typografie
- Heading-Font + Body-Font (Vorschlag aus typography.csv/google-fonts) + Begründung

## Bildsprache & Layout
- Fotostil, Formen/Ecken, Dichte, Sektionsreihenfolge (aus landing.csv/Beispielen)

## Beispiel-Websites (Orientierung)
1. <URL> — was daran gut ist: <…>
2. …

## Do / Don't für diese Nische
- Do: <…>
- Don't: <…>
```

Speichere nach `<shop>/design-anforderungen.md`.
