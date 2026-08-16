# Local Shop Website Generator

Claude-Code-Skill, der über Google Maps einen lokalen Betrieb **ohne eigene Website** findet,
ihn recherchiert und ihm vollautomatisch eine fertige statische Website baut.

Der Ablauf läuft **autonom** durch — die einzige mögliche Rückfrage ist der Standort, falls er
weder automatisch bestimmbar ist noch in `standort.md` steht.

## Ablauf

| Schritt | Ergebnis |
|---|---|
| 0 | Standort bestimmen → `standort.md` |
| 1 | Maps-Suche nach einem Betrieb ohne Website (nicht in `archiv.md`) |
| 2 | Shop-Recherche → `<shop>/Daten.md` |
| 3 | Website-Spezifikation → `<shop>/website-spezifikation.md` |
| 4 | Design-Recherche (Nische) → `<shop>/design-anforderungen.md` |
| 5 | Design im Google-Stitch-Format → `<shop>/Design.md` |
| 6–7 | Statische Website (HTML + Tailwind) → `<shop>/website/` |
| 8 | Eintrag ins Archiv → `archiv.md` |

Ein Shop pro Durchlauf. Alle Dateien liegen relativ zum aktuellen Arbeitsverzeichnis.

## Grundregeln

- **Keine erfundenen Daten.** Nur verifizierte Infos landen auf der Website; Fehlendes wird als
  Platzhalter gekennzeichnet.
- **Nichts wird veröffentlicht.** Der Skill erzeugt nur lokale Dateien — kein Deploy, keine
  Nachrichten, keine Einträge irgendwo. Deployen ist Sache des Users.
- **Datensparsam browsen.** Nur öffentliche Brancheneinträge, Consent-Banner immer ablehnen,
  keine Logins, keine Formulare, keine CAPTCHAs.

## Struktur

```
SKILL.md            Hauptanleitung (Ablauf, Regeln, Checkliste)
references/         Detailanleitungen je Schritt (Maps, Recherche, Spec, Design, Bau)
templates/          Vorlagen für Daten.md, Spezifikation, Design-Anforderungen, Design.md
engine/             gebündelte ui-ux-pro-max-Design-Engine (Skripte + CSV-Wissensbasis)
```

`ui-ux-pro-max` ist vollständig integriert (inkl. No-Python-Fallback) — es wird kein weiterer
Skill benötigt.

## Installation

Repo nach `~/.claude/skills/local-shop-website-generator` klonen:

```bash
git clone <repo-url> ~/.claude/skills/local-shop-website-generator
```

Danach steht der Skill in Claude Code als `local-shop-website-generator` zur Verfügung.
