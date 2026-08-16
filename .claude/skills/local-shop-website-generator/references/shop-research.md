# Referenz: Shop-Tiefenrecherche → `Daten.md`

Ziel: alles zusammentragen, was über **genau diesen** Betrieb öffentlich auffindbar ist, und es
quellenbasiert in `<shop>/Daten.md` festhalten. Diese Datei ist die **einzige Wahrheitsquelle** für die
spätere Website — was hier nicht steht (und nicht als bestätigt markiert ist), darf **nicht** auf die
Website.

## Ordner anlegen
Lege `<shop>/` im Workspace an. Ordnername = echter Shop-Name, bereinigt um `\ / : * ? " < > |` und
getrimmt. Beispiel: `Bäckerei Krönert & Sohn` → Ordner `Bäckerei Krönert & Sohn`.

## Recherchequellen (in dieser Reihenfolge)
1. **Maps-Panel** (aus Schritt 1): Name, Adresse, Telefon, Öffnungszeiten, Kategorie, Bewertung,
   Rezensionen, Fotos. Öffne bei Bedarf im Browser erneut den Eintrag und lies Details/Rezensionen.
2. **Websuche** (`WebSearch`) nach `"<Name>" <Ort>` und Varianten (`<Name> Speisekarte`,
   `<Name> Instagram`, `<Name> Facebook`, `<Name> Öffnungszeiten`).
3. **Social Media**: Instagram-/Facebook-Profil des Betriebs (Angebote, Bilder, Beschreibung, Aktuelles).
4. **Branchen-/Bewertungsportale**: z.B. Gelbe Seiten, Yelp, TripAdvisor, Lieferdienst-Seiten,
   Branchenverzeichnisse. `WebFetch` auf die relevanteste Seite für Detailinfos.

## Den richtigen Betrieb sicherstellen
Verifiziere über **Adresse + Telefon**, dass eine Quelle wirklich zu diesem Betrieb gehört — nicht zu
einem namensgleichen in einer anderen Stadt. Passt eine Quelle nicht eindeutig, kennzeichne sie als
„nicht sicher zuzuordnen" oder lass sie weg.

## Umgang mit Unsicherheit
- Jede Angabe bekommt eine **Quelle** (Maps / Instagram / Website X …).
- Widersprechen sich Quellen (z.B. Öffnungszeiten), notiere beide und markiere als **„zu bestätigen"**.
- **Nichts erfinden.** Lieber „nicht auffindbar" schreiben als raten.

## `Daten.md` — Template
Nutze diese Struktur (Vorlage auch unter `templates/Daten.template.md`):

```markdown
# Daten – <Name des Shops>

## Stammdaten
- **Name:** <exakter Name>
- **Branche/Kategorie:** <…>
- **Adresse:** <Straße Nr., PLZ Ort>
- **Telefon:** <…>
- **E-Mail:** <… oder "nicht auffindbar">
- **Öffnungszeiten:** <… (Quelle) | zu bestätigen>
- **Preisniveau:** <€/€€/€€€ falls bekannt, sonst weglassen>

## Angebot / Leistungen / Speisekarte
- <Leistung/Produkt> — <Detail> _(Quelle)_
- …

## Über den Betrieb (Story / USP)
- Gründung/Geschichte, Inhaber, Besonderheiten, Auszeichnungen _(je Quelle)_
- Alleinstellungsmerkmale (z.B. handgemacht, regional, seit …)

## Reputation
- **Bewertung:** <Ø / Anzahl> _(Maps)_
- Wiederkehrende Lob-/Kritikpunkte aus Rezensionen (Stichworte, keine Zitate erfinden)

## Präsenz & Assets
- **Website:** keine (Grund der Bearbeitung)
- **Social Media:** <Instagram/Facebook-Links oder "keine gefunden">
- **Fotos:** <vorhanden? Motive: Interieur, Produkte, Team …> _(Quelle)_
- **Logo/Marke:** <vorhanden? Farben/Stil, falls erkennbar>

## Lage / Anfahrt
- <ÖPNV, Parken, Stadtteil, Umgebung> _(falls auffindbar)_

## Offene Punkte / zu bestätigen
- <alles Unsichere gesammelt — wird später zu Website-Platzhaltern>

## Quellen
- <Liste der genutzten URLs/Quellen>
```

Speichere das Ergebnis nach `<shop>/Daten.md`.
