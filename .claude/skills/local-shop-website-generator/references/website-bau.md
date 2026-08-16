# Referenz: Website bauen (statisch, HTML + Tailwind)

Ziel: aus `Design.md` (Vorgabe), `Daten.md` (Inhalt) und `website-spezifikation.md` (was rein/raus)
eine fertige, **self-contained** statische Website nach `<shop>/website/` bauen — **vollautomatisch,
ohne Rückfrage**. Sie muss per Doppelklick auf `index.html` öffnen, responsiv und barrierefrei sein.

Nutze parallel `references/ui-ux-pro-max.md` (Design-Intelligence + Quick-Reference-Checklisten).

## Vorgehen
1. **Design-System holen (integriertes ui-ux-pro-max).**
   - Mit Python: `python engine/scripts/search.py "<branche> <keywords>" --design-system -p "<Shop>"`
     — als Absicherung/Ergänzung zu `Design.md`.
   - Ohne Python: Fallback laut `references/ui-ux-pro-max.md` (Quick Reference + CSVs in `engine/data/`).
2. **Tokens aus `Design.md` übernehmen** (Farben, Typo, Spacing, Radius, Schatten) — 1:1, als harte
   Vorgabe. Keine abweichenden Farben/Fonts erfinden.
3. **Inhalte aus `Daten.md`** gemäß `website-spezifikation.md` einsetzen. Platzhalter aus der Spec
   sichtbar als solche darstellen (z.B. dezenter Hinweis-Text), **nichts erfinden**.
4. **Bauen** (Struktur unten), dann gegen die **Qualitäts-Checkliste** prüfen.

## Dateistruktur in `<shop>/website/`
```
website/
├── index.html          # One-Pager mit allen Sektionen aus der Spec
├── impressum.html      # Platzhalter-Rechtsseite (vom Inhaber auszufüllen)
├── datenschutz.html    # Platzhalter-Rechtsseite
└── assets/             # optional: eigenes SVG-Logo/Icons/favicon (nur selbst erzeugte Assets)
```

## Technik-Vorgaben
- **Tailwind ohne Build:** Tailwind Play CDN einbinden und die `Design.md`-Tokens konfigurieren:
  ```html
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = { theme: { extend: { colors: {
      primary: 'var(--color-primary)', accent: 'var(--color-accent)',
      surface: 'var(--color-surface)', /* … alle Tokens … */ } } } };
  </script>
  <style>
    :root{ --color-primary:#...; --color-accent:#...; --color-surface:#...; /* aus Design.md */ }
  </style>
  ```
  So sind die semantischen Tokens an **einer** Stelle definiert (CSS-Variablen) und via Tailwind nutzbar.
- **Fonts:** gewählte Google Fonts per `<link>` einbinden; `font-display: swap`.
- **Meta:** `<!doctype html>`, `<html lang="de">`, `<meta name="viewport" content="width=device-width, initial-scale=1">`, sinnvoller `<title>` + Meta-Description, Open-Graph-Basis.
- **Semantik:** `header/nav/main/section/footer`, eine `h1`, saubere Heading-Hierarchie, `alt`-Texte,
  `aria-label` für Icon-Buttons, sichtbare Fokus-Ringe.
- **Responsiv:** mobile-first, Breakpoints aus `Design.md`, kein horizontales Scrollen, `min-h-dvh`.

## Bilder & Karte (wichtig — Integrität & Rechte)
- **Fotos NICHT automatisch herunterladen.** Die Fotos des Betriebs (Google/Social) sind fremd und
  das Herunterladen von Dateien ist ohne ausdrückliche Freigabe tabu. Verwende stattdessen **dezente
  Platzhalter-Flächen** (z.B. Tailwind-Gradient/Neutralfläche mit passendem Icon und beschreibendem
  Alt-Text, z.B. „Foto: Ladenlokal — vom Inhaber einzufügen"). Keine Stockfotos, die echte Zustände
  vortäuschen. So bleibt die Seite ehrlich und der Inhaber sieht, wo seine echten Bilder hinkommen.
- **Karte** ohne API-Key: OpenStreetMap-Embed per iframe auf die Adresse, plus Text-Link „Auf Google
  Maps ansehen". Beispiel-iframe:
  ```html
  <iframe title="Karte" loading="lazy" class="w-full h-72 rounded-lg border-0"
    src="https://www.openstreetmap.org/export/embed.html?bbox=<lon1>,<lat1>,<lon2>,<lat2>&marker=<lat>,<lon>"></iframe>
  ```
  Koordinaten grob aus der Adresse ableiten; wenn unsicher, stattdessen prominenter Adress-Block +
  „Route planen"-Link (`https://www.google.com/maps/dir/?api=1&destination=<url-encoded-adresse>`).
- **Logo:** wenn kein echtes Logo vorliegt, eine schlichte **Wortmarke** (Name in der Heading-Font) —
  kein fremdes Logo nachbauen.

## Inhaltliche Ehrlichkeit
- Nur Aussagen, die durch `Daten.md` gedeckt sind. Keine erfundenen Bewertungen, Preise, Zitate,
  Öffnungszeiten, Auszeichnungen. Unbestätigtes → sichtbarer Platzhalter.
- Rechtsseiten (`impressum.html`, `datenschutz.html`) enthalten nur einen klaren Platzhalter-Hinweis,
  **keine** erfundenen Rechtstexte.

## Qualitäts-Checkliste (vor Abschluss prüfen — Quick Reference §1–§10)
- [ ] Öffnet fehlerfrei; keine Konsolenfehler; kein horizontales Scrollen auf 375px
- [ ] Textkontrast ≥ 4.5:1; sichtbare Fokuszustände; sinnvolle `alt`-Texte
- [ ] Touch-Ziele ≥ 44px; Buttons haben Hover-/Fokus-/Aktiv-Zustände
- [ ] Genau eine `h1`, saubere Heading-Hierarchie, semantische Landmarks
- [ ] Tokens/Fonts exakt aus `Design.md`; keine Emojis als Icons (SVG nutzen)
- [ ] Alle Inhalte durch `Daten.md` gedeckt; Platzhalter klar markiert
- [ ] Telefon als `tel:`-Link, Route-Link funktioniert, Karte lädt
- [ ] `prefers-reduced-motion` respektiert; Animationen 150–300ms

## Verifikation (wenn möglich)
Öffne die fertige `index.html` im eingebauten Browser (`preview_start`/`navigate` auf den `file:///`-Pfad),
prüfe Darstellung mobil (`resize_window` preset `mobile`) und Konsole (`read_console_messages`). Ist das
in der Sandbox nicht möglich, prüfe den HTML-Code sorgfältig gegen die Checkliste oben. Verifikation ist
Kür — der Bau darf daran nicht scheitern.
