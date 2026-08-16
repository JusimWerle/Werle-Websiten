---
name: local-shop-website-generator
description: >-
  Findet über Google Maps lokale Shops, Gastronomie & Dienstleister OHNE eigene Website und
  erstellt ihnen vollautomatisch eine komplette Website. Nutze diesen Skill immer, wenn der User
  lokale Betriebe / Läden / Restaurants / Cafés / Handwerker ohne Homepage finden will, Website-Leads
  oder Akquise für lokale Unternehmen braucht, "einen Shop ohne Website" sucht, oder aus einem
  Maps-Eintrag automatisch Recherche, Spezifikation, Design und eine fertige Website bauen will.
  Deckt den ganzen Ablauf ab: Standort bestimmen → Maps-Suche nach Betrieben ohne Website →
  Shop-Recherche (Daten.md) → Website-Spezifikation → Design-Recherche → Design.md im Google-Stitch-
  Format → statische Website (HTML + Tailwind) → Eintrag ins Archiv. Trigger u.a.: "Shop ohne Website",
  "lokale Website-Akquise", "Google Maps Leads", "bau einer lokalen Firma eine Website",
  "find a local business without a website and build it a site".
---

# Local Shop Website Generator

Dieser Skill führt einen **vollständig autonomen** End-to-End-Ablauf aus: Er findet über Google Maps
einen lokalen Betrieb **ohne eigene Website**, recherchiert alles Auffindbare über genau diesen Betrieb,
schreibt daraus eine Datengrundlage, eine Website-Spezifikation, Design-Anforderungen und eine
`Design.md` im Google-Stitch-Format, und baut daraus eine fertige statische Website (HTML + Tailwind)
in einem eigenen Ordner. Am Ende wird der Betrieb ins Archiv eingetragen, damit er nicht erneut
bearbeitet wird.

Der `ui-ux-pro-max`-Design-Skill ist **vollständig in diesen Skill integriert** (siehe
`engine/` und `references/ui-ux-pro-max.md`). Du brauchst keinen weiteren Skill.

## Grundregeln (unbedingt beachten)

1. **Keine Rückfragen.** Arbeite den kompletten Ablauf autonom durch und triff sinnvolle
   Entscheidungen selbst. Frage den User **nur in einem einzigen Fall**: wenn der Standort weder
   automatisch bestimmbar ist noch in `standort.md` steht (siehe Schritt 0). Sonst niemals anhalten,
   niemals um Bestätigung bitten — auch nicht bei Zwischenergebnissen.
2. **Workspace = aktuelles Arbeitsverzeichnis.** Alle Dateien/Ordner (`standort.md`, `archiv.md`,
   `<shop>/…`) liegen relativ zum aktuellen Arbeitsverzeichnis. Prüfe zu Beginn per Verzeichnis-Listing,
   was schon existiert.
3. **Ein Shop pro Durchlauf.** Finde **einen** passenden Betrieb, verarbeite ihn komplett bis zur
   fertigen Website, trage ihn ins Archiv ein — fertig. Nicht mehrere Shops in einem Lauf.
4. **Keine erfundenen Daten (Integrität).** Auf die Website und in alle `.md`-Dateien kommen nur
   Informationen, die du wirklich verifiziert hast. Erfinde keine Preise, Öffnungszeiten, Bewertungen,
   Zitate, Team-Namen oder Angebote. Fehlt etwas, kennzeichne es als Platzhalter — lüge nicht.
5. **Nur lokale Dateien, kein Veröffentlichen.** Der Skill erzeugt Dateien im Workspace. Er
   deployt/veröffentlicht nichts, verschickt nichts und trägt nirgends etwas ein. Das Deployen ist
   Sache des Users.
6. **Datensparsam & sicher browsen.** Beim Maps-Zugriff nur öffentliche Brancheneinträge lesen.
   Consent-/Cookie-Banner immer mit der datensparsamsten Option schließen (**„Alle ablehnen"**,
   niemals „Alle akzeptieren"). Keine Logins, keine Formulare absenden, keine CAPTCHAs lösen.

## Ablauf im Überblick

```
Schritt 0  Standort bestimmen        → standort.md (nur bei Bedarf anlegen/fragen)
Schritt 1  Maps: Shop ohne Website   → einen Kandidaten wählen (nicht in archiv.md)
Schritt 2  Ordner + Recherche        → <shop>/Daten.md
Schritt 3  Website-Spezifikation     → <shop>/website-spezifikation.md
Schritt 4  Design-Recherche (Nische) → <shop>/design-anforderungen.md
Schritt 5  Design im Stitch-Format   → <shop>/Design.md
Schritt 6  Website-Ordner anlegen    → <shop>/website/
Schritt 7  Website bauen (integr. ui-ux-pro-max) → <shop>/website/index.html …
Schritt 8  Archiv aktualisieren      → archiv.md (anlegen falls nicht vorhanden)
```

Jeder Schritt hat eine ausführliche Anleitung in `references/`. Lies die jeweils genannte Datei,
**bevor** du den Schritt ausführst — sie enthält die Details, Formate und Fallstricke.

---

## Schritt 0 — Standort bestimmen

Die Maps-Suche muss sich am Standort des Users orientieren. Bestimme ihn in **dieser Reihenfolge**
und höre beim ersten Erfolg auf:

1. **`standort.md` lesen.** Existiert die Datei im Workspace und enthält einen Ort? → benutze ihn.
   Fertig, keine Rückfrage.
2. **Automatisch bestimmen (Best-Effort).** Gibt es keine `standort.md`, versuche den Standort
   automatisch zu ermitteln. Beachte: In dieser Umgebung ist eine echte GPS-/Geolokalisierung meist
   **nicht** möglich (Netzwerk-/Server-IP ≠ User-Standort). Nutze ein Ergebnis nur, wenn es klar
   plausibel ist. Im Zweifel gilt: nicht bestimmbar.
3. **Genau einmal fragen.** Nur wenn 1 und 2 fehlschlagen: frage den User **einmal** kurz nach seinem
   Standort (Stadt/Stadtteil oder Adresse und optional Umkreis). Das ist die **einzige** erlaubte
   Rückfrage im ganzen Skill.
4. **Persistieren.** Sobald ein Standort feststeht (egal ob aus Schritt 2 oder 3), schreibe ihn nach
   `standort.md` (anlegen, falls nicht vorhanden), damit künftige Läufe ihn ohne Nachfrage nutzen.

`standort.md`-Format (einfach halten):

```markdown
# Standort
Ort: <Stadt / Stadtteil oder Adresse>
Umkreis: <optional, z.B. 3 km>
```

---

## Schritt 1 — Auf Google Maps einen Shop ohne Website finden

**Lies zuerst `references/google-maps-recherche.md`** — dort steht Schritt für Schritt, wie du mit dem
eingebauten Browser (Claude-Browser-Tools: `preview_start`/`navigate`, `read_page`, `find`, `computer`)
Google Maps bedienst, den Consent-Banner ablehnst, Brancheneinträge durchgehst und erkennst, ob ein
Eintrag eine Website hat.

Kurzfassung:
- Öffne Google Maps und suche eine lokale Branche (z.B. Friseur, Bäckerei, Café, Restaurant,
  Kosmetik, Handwerk, Blumenladen …) am Standort aus Schritt 0. Variiere Branche/Suchbegriff, bis du
  einen passenden Betrieb findest.
- Ein Eintrag ist ein **Kandidat**, wenn er **keinen „Website"-Button / keine Website-URL** hat, aber
  ein echter Betrieb ist (Name + Adresse vorhanden; idealerweise Telefon/Öffnungszeiten).
- **Archiv-Abgleich:** Lies `archiv.md` (falls vorhanden). Überspringe jeden Kandidaten, der dort schon
  steht (Abgleich über Name **und** Adresse, tolerant gegenüber Schreibweisen).
- Wähle **den ersten** passenden Kandidaten, der nicht im Archiv steht. Notiere alle im Maps-Panel
  sichtbaren Fakten (Name, Adresse, Telefon, Öffnungszeiten, Kategorie, Bewertung, Bilder) — sie sind
  die Basis für Schritt 2.

Wenn eine Suche nichts liefert, probiere andere Branchen/Stadtteile — **nicht** aufgeben und **nicht**
nachfragen.

---

## Schritt 2 — Ordner anlegen & Shop recherchieren → `Daten.md`

**Lies `references/shop-research.md`.**

- Lege im Workspace den Ordner `<shop>/` an. Ordnername = echter Name des Shops, bereinigt um die
  Zeichen `\ / : * ? " < > |` und getrimmt (Umlaute/Leerzeichen dürfen bleiben).
- Recherchiere **alles**, was du zu **genau diesem** Betrieb findest: die Maps-Fakten aus Schritt 1
  plus Websuche nach Name + Ort (Social Media wie Instagram/Facebook, Branchenverzeichnisse,
  Speisekarten, Presse, Fotos, Angebote, Geschichte/Über-uns, Team).
- Achte darauf, den **richtigen** Betrieb zu erwischen (gleiche Adresse/Telefon), nicht einen
  namensgleichen woanders.
- Schreibe das Ergebnis nach `<shop>/Daten.md`. Struktur/Template siehe `references/shop-research.md`.
  Kennzeichne jede Angabe mit ihrer Quelle und markiere Unsicheres klar als unbestätigt.

---

## Schritt 3 — Website-Spezifikation → `website-spezifikation.md`

**Lies `references/website-spezifikation.md`.**

Entscheide auf Basis von `Daten.md`, **welche** Inhalte auf die Website gehören und **welche nicht**,
und lege die Seitenstruktur fest (z.B. Hero, Leistungen/Speisekarte, Über uns, Galerie, Öffnungszeiten,
Kontakt/Anfahrt mit Karte, Footer mit Impressumshinweis). Halte fest:
- **Rein:** verifizierte, für Kunden relevante Infos.
- **Raus:** unbestätigte Daten, sensible/private Details, alles Erfundene, rechtlich Heikles
  (keine falschen Gütesiegel, keine erfundenen Bewertungen).
- **Platzhalter:** was fehlt, aber gebraucht wird (z.B. „Öffnungszeiten bitte bestätigen").

Speichere das nach `<shop>/website-spezifikation.md`.

---

## Schritt 4 — Design-Recherche zur Nische → `design-anforderungen.md`

**Lies `references/design-recherche.md`.**

Recherchiere, welches Design zur Branche/Nische des Shops passt (Stimmung, Farbwelt, Typografie,
Bildsprache, Layout-Konventionen) und sammle 2–4 Beispiel-Websites erfolgreicher Betriebe derselben
Nische zur Orientierung. Nutze dafür Websuche **und** die integrierte Design-Intelligence
(`references/ui-ux-pro-max.md` bzw. `engine/scripts/search.py --design-system`, mit Python-Fallback).
Ergebnis nach `<shop>/design-anforderungen.md`.

---

## Schritt 5 — `Design.md` im Google-Stitch-Format

**Lies `references/design-md-stitch-format.md`.**

Übersetze `design-anforderungen.md` in eine `Design.md`, die dem **Google-Stitch-DESIGN.md-Format**
entspricht: High-Level-Konzept & Vibe, Farb-System mit **semantischen Tokens + Hex**, Typografie
(Font-Familien, Größen, Gewichte, Zeilenhöhen), Spacing-Scale, Border-Radius/Schatten, Komponenten und
pro Sektion/Screen die Layout-Hierarchie. Das Format und ein vollständiges Template stehen in der
Referenz. Speichere nach `<shop>/Design.md`.

---

## Schritt 6 — Website-Ordner anlegen

Lege `<shop>/website/` an. (Nur der Ordner — die Dateien entstehen in Schritt 7.)

---

## Schritt 7 — Website bauen (integriertes ui-ux-pro-max)

**Lies `references/website-bau.md`** (Bau-Anleitung) **und** nutze `references/ui-ux-pro-max.md`
(Design-Intelligence & UX-Qualitätsregeln).

Baue aus den drei Dateien `Design.md`, `Daten.md` und `website-spezifikation.md` **vollautomatisch**
eine fertige, statische Website nach `<shop>/website/`:
- **Stack:** statisches **HTML + Tailwind** (self-contained, kein Build-Schritt, öffnet per Doppelklick
  auf `index.html`).
- Halte dich strikt an die Tokens/Struktur aus `Design.md`, fülle sie mit den echten Inhalten aus
  `Daten.md` gemäß `website-spezifikation.md`.
- Wende die integrierte ui-ux-pro-max-Design-Intelligence an: wenn Python verfügbar ist, hol dir mit
  `engine/scripts/search.py "<nische> <keywords>" --design-system` die Design-System-Empfehlung; sonst
  nutze den Fallback (Quick Reference §1–§10 + CSVs). Prüfe das Ergebnis gegen die Quick-Reference-
  Checklisten (Barrierefreiheit, Touch-Ziele, Responsivität, Typografie/Farbe, Motion).
- Ergebnis muss **responsiv** und **barrierefrei** sein und real öffnen. Details/Grundgerüst in
  `references/website-bau.md`.

---

## Schritt 8 — Archiv aktualisieren → `archiv.md`

Trage den bearbeiteten Betrieb in `archiv.md` im Workspace ein (Datei anlegen, falls nicht vorhanden),
damit er in künftigen Läufen übersprungen wird. Ein Eintrag pro Zeile mit Name **und** Adresse:

```markdown
# Archiv – bearbeitete Shops
- **<Name des Shops>** — <vollständige Adresse> (bearbeitet am <YYYY-MM-DD>)
```

Beim Anlegen die Überschrift mitschreiben; bei vorhandener Datei nur die neue Zeile anhängen.

---

## Definition of Done (Selbstkontrolle vor Abschluss)

Prüfe, dass alles existiert und gefüllt ist, dann fasse dem User das Ergebnis kurz zusammen:

- [ ] `standort.md` vorhanden und mit Ort gefüllt
- [ ] `<shop>/Daten.md` — recherchierte, quellenbasierte Daten (nichts erfunden)
- [ ] `<shop>/website-spezifikation.md` — Inhalte drin/raus + Seitenstruktur
- [ ] `<shop>/design-anforderungen.md` — Nischen-Design + Beispiel-Websites
- [ ] `<shop>/Design.md` — im Google-Stitch-Format (Tokens, Typo, Spacing, Komponenten, Layout)
- [ ] `<shop>/website/` — fertige, öffnende, responsive HTML+Tailwind-Website
- [ ] `archiv.md` — enthält den Betrieb mit Name + Adresse
- [ ] Keine Rückfrage gestellt (außer ggf. der Standort in Schritt 0)

## Referenzdateien

- `references/google-maps-recherche.md` — Maps per Browser bedienen; Website-Erkennung; Archiv-Abgleich
- `references/shop-research.md` — Tiefenrecherche zu einem Betrieb; `Daten.md`-Template
- `references/website-spezifikation.md` — was auf die Seite gehört (und was nicht); `website-spezifikation.md`-Template
- `references/design-recherche.md` — Nischen-Design recherchieren; `design-anforderungen.md`-Template
- `references/design-md-stitch-format.md` — Google-Stitch-`Design.md`-Format + Template
- `references/website-bau.md` — statische HTML+Tailwind-Website bauen; Grundgerüst
- `references/ui-ux-pro-max.md` — **integrierte** Design-Intelligence + UX-Qualitätsregeln (§1–§10)
- `engine/` — gebündelte ui-ux-pro-max-Scripts (`engine/scripts/`) + Daten (`engine/data/`)
- `templates/` — Kopiervorlagen für die vier `.md`-Ausgabedateien
