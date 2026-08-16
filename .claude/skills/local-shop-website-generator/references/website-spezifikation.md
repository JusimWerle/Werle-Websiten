# Referenz: Website-Spezifikation → `website-spezifikation.md`

Ziel: aus `Daten.md` festlegen, **welche** Inhalte auf die Website gehören, **welche nicht**, und
**wie** die Seite strukturiert ist. Diese Datei ist die Brücke zwischen Rohdaten und Bau — sie
verhindert, dass Unbestätigtes oder Erfundenes auf die Seite rutscht.

## Leitprinzipien
- **Kundenfokus:** rein kommt, was ein potenzieller Kunde sehen will (Was gibt's? Wo? Wann offen?
  Wie kontaktieren?).
- **Nur Verifiziertes:** jede Aussage muss durch `Daten.md` gedeckt sein. Unbestätigtes wird zum
  **Platzhalter**, nicht zur Behauptung.
- **Ehrlichkeit vor Vollständigkeit:** keine erfundenen Bewertungen, Gütesiegel, Preise, Teamnamen,
  Jahreszahlen. Kein rechtlich Heikles.
- **Ein klares Primärziel** pro Seite (meist: anrufen / vorbeikommen).

## Inhalte einordnen: Rein / Raus / Platzhalter
Ordne für diesen konkreten Shop jede Info einer Kategorie zu:

- **Rein (verifiziert):** Name, Branche, Adresse, Karte, Telefon, Öffnungszeiten (falls bestätigt),
  reale Leistungen/Produkte, echte USPs, vorhandene Fotos/Social-Links.
- **Raus:** widersprüchliche/unbestätigte Daten, sensible/private Details, alles Erfundene, unklare
  Rechtsangaben.
- **Platzhalter (sichtbar markiert):** was gebraucht wird, aber fehlt — z.B. „[Öffnungszeiten bitte
  bestätigen]", „[E-Mail ergänzen]", „[Foto folgt]". So sieht der Inhaber sofort, was noch fehlt.

## Seitenstruktur festlegen
Wähle passende Sektionen (typisch für lokale Einseiter). Nicht alle sind immer nötig:

1. **Header/Nav** — Name/Logo, Anker-Links, Telefon-CTA
2. **Hero** — Name, knappe Positionierung, Primär-CTA (Anrufen/Route), 1 starkes Bild
3. **Leistungen / Speisekarte / Sortiment** — echte Angebote aus `Daten.md`
4. **Über uns** — Story/USP (nur belegt)
5. **Galerie** — vorhandene Fotos (sonst weglassen, nicht mit Stockbildern faken)
6. **Öffnungszeiten** — falls bestätigt, sonst Platzhalter
7. **Kontakt & Anfahrt** — Adresse, Telefon, eingebettete Karte, ÖPNV/Parken
8. **Footer** — Copyright, Hinweis auf nötiges Impressum/Datenschutz (Platzhalter, s.u.)

## Rechtliches (DE-Kontext)
Deutsche Websites brauchen i.d.R. **Impressum** und **Datenschutzerklärung**. Der Skill kennt nicht
alle rechtlichen Pflichtangaben des Betriebs → lege **Platzhalter-Seiten/Abschnitte** an
(`[Impressum – vom Inhaber auszufüllen]`, `[Datenschutzerklärung – rechtssicher ergänzen]`) und
erfinde **keine** Rechtstexte. Verlinke sie im Footer.

## `website-spezifikation.md` — Template
(Vorlage auch unter `templates/website-spezifikation.template.md`)

```markdown
# Website-Spezifikation – <Name des Shops>

## Ziel & Zielgruppe
- Primärziel der Seite: <z.B. Anrufe/Laufkundschaft>
- Zielgruppe: <…>

## Seitenstruktur (Sektionen in Reihenfolge)
1. <Sektion> — Inhalt: <…> — CTA: <…>
2. …

## Inhalte: REIN (verifiziert)
- <Info> _(Quelle in Daten.md)_

## Inhalte: RAUS (bewusst weggelassen)
- <Info> — Grund: <unbestätigt / privat / erfunden / rechtlich>

## Platzhalter (fehlt, wird markiert dargestellt)
- <z.B. Öffnungszeiten bestätigen, E-Mail, weitere Fotos>

## Kontakt & Conversion
- Telefon-CTA, Route/Karte, ggf. Social-Links

## Rechtliches
- Impressum: Platzhalter
- Datenschutz: Platzhalter

## Technische Vorgaben
- Statisches HTML + Tailwind, responsiv, barrierefrei, Deutsch, kein Build-Schritt
```

Speichere nach `<shop>/website-spezifikation.md`.
