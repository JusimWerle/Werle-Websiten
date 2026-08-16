# Referenz: Google Maps – Shops ohne Website finden

Ziel: über den **eingebauten Browser** (Claude-Browser-Tools) auf Google Maps einen lokalen Betrieb
finden, der **keine eigene Website** hat und noch **nicht in `archiv.md`** steht. Genau **einen**
Kandidaten wählen und seine öffentlich sichtbaren Fakten notieren.

Der Browser läuft in einer Sandbox. Arbeite bevorzugt mit der **Accessibility-Tree-Ausgabe**
(`read_page`) statt mit Screenshots — sie ist präziser und zeigt Button-Beschriftungen wie „Website".

## Genutzte Tools (In-App-Browser)

| Tool | Zweck |
|------|-------|
| `mcp__Claude_Browser__preview_start` `{url}` | Browser-Tab öffnen (falls noch keiner offen ist) |
| `mcp__Claude_Browser__navigate` `{tabId:"main", url}` | zu einer URL navigieren |
| `mcp__Claude_Browser__read_page` `{tabId:"main", filter:"interactive"}` | Seite als Accessibility-Tree mit `ref_N` lesen |
| `mcp__Claude_Browser__find` `{tabId:"main", query}` | Element per Beschreibung finden → `ref_N` |
| `mcp__Claude_Browser__computer` `{tabId:"main", action}` | klicken/scrollen/tippen (per `ref` oder `coordinate`) |
| `mcp__Claude_Browser__get_page_text` `{tabId:"main"}` | Sichttext extrahieren (Adressen, Telefon etc.) |

## Ablauf

### 1. Suche öffnen
Baue eine Maps-Such-URL aus **Branche + Standort** (Standort aus Schritt 0). URL-Format:

```
https://www.google.com/maps/search/<branche>+<ort>
```

Beispiel: `https://www.google.com/maps/search/Friseur+Bonn+Beuel`
(Leerzeichen als `+`, Umlaute funktionieren; alternativ URL-encoden.)

Öffne per `preview_start {url: "<such-url>"}` (oder `navigate`, falls schon ein Tab offen ist).

**Branchen-Ideen** (variiere, bis du fündig wirst — kleine, inhabergeführte Betriebe haben oft keine
Website): Friseur, Barbier, Nagelstudio, Kosmetik, Bäckerei, Metzgerei, Café, Restaurant, Imbiss,
Eisdiele, Blumenladen, Änderungsschneiderei, Schuhmacher, Reinigung, Fahrradladen, Kfz-Werkstatt,
Fußpflege, Massage, Physiotherapie, Tattoo-Studio, Antiquariat, Weinhandlung.

### 2. Consent-/Cookie-Banner ablehnen
In der EU zeigt Google zuerst einen Einwilligungs-Dialog. **Datensparsam schließen:**
`find {query:"Alle ablehnen button"}` → mit `computer {action:"left_click", ref}` klicken.
Niemals „Alle akzeptieren". Falls kein Banner erscheint, weiter.

### 3. Ergebnisliste durchgehen
`read_page {filter:"interactive"}` liefert die Trefferliste (Feed) als Links mit Betriebsnamen.
Gehe die Treffer der Reihe nach durch. Zum Nachladen weiterer Treffer im Feed nach unten scrollen:
`computer {action:"scroll", scroll_direction:"down", coordinate:[<x im Feed>, <y>]}`.

### 4. Pro Treffer: Website-Check (Kernlogik)
Öffne den Treffer (`computer {action:"left_click", ref}` auf den Namen) → Detail-Panel lädt →
`read_page {filter:"interactive"}` **und** `get_page_text`.

Entscheide, ob der Betrieb eine **Website** hat:

- **HAT eine Website** (→ überspringen), wenn im Detail-Panel ein Aktions-Button/Link **„Website"**
  (Globus-Icon) vorhanden ist bzw. eine echte Domain angezeigt wird (z.B. `beispiel-friseur.de`).
- **KEINE Website** (→ **Kandidat**), wenn **kein** „Website"-Button existiert. Häufig steht dann
  stattdessen ein Hinweis wie **„Website hinzufügen"** / „Als Inhaber eintragen" — starkes Signal für
  fehlende Website.

Zusätzlich muss der Kandidat ein **echter Betrieb** sein: Name + Adresse vorhanden, idealerweise
Telefonnummer und/oder Öffnungszeiten. Reine „In dieser Gegend"-Platzhalter ohne Adresse ignorieren.

> Hinweis: Verlinkt der „Website"-Button nur auf ein Social-Media-Profil, zählt das hier trotzdem als
> „hat Website" (Maps führt es als Website). Ziel sind Betriebe **ganz ohne** Website-Feld. Ob der
> Betrieb sonst nur bei Instagram/Facebook auftaucht, klärt die Tiefenrecherche in Schritt 2.

### 5. Archiv-Abgleich
Bevor du einen Kandidaten endgültig wählst: lies `archiv.md` im Workspace (falls vorhanden). Steht der
Kandidat dort schon (Abgleich über **Name UND Adresse**, tolerant gegenüber Schreibweise/Abkürzungen)
→ überspringen und nächsten Treffer prüfen.

### 6. Kandidat festlegen & Fakten sichern
Nimm **den ersten** Betrieb, der (a) keine Website hat, (b) ein echter Betrieb ist und (c) nicht im
Archiv steht. Sichere **alle** im Panel sichtbaren Fakten für Schritt 2:

- Exakter Name, vollständige Adresse, Telefon
- Kategorie/Branche, Öffnungszeiten
- Bewertung + Anzahl Rezensionen, ggf. einzelne Rezensionstexte
- Ob Fotos vorhanden sind (Anzahl, Motive)
- Plus-Code / grobe Lage, ggf. sichtbare Merkmale („Bio", „seit 1998" etc.)

## Robustheit & Grenzen
- Findet eine Branche nichts Passendes, **wechsle Branche/Stadtteil** — nicht aufgeben, nicht fragen.
- Lädt eine Seite langsam, kurz warten (`computer {action:"wait", duration:2}`) und `read_page` erneut.
- Zeigt Maps eine „ungewöhnlicher Traffic"/CAPTCHA-Seite: **kein CAPTCHA lösen.** Neu laden oder Suche
  variieren; hilft das nicht, dem User das Problem sachlich melden (kein Abbruch mit Rückfrage nötig,
  aber ehrlich berichten).
- Nur öffentliche Brancheninfos lesen. Keine Logins, keine Formulare, keine privaten Daten sammeln.
