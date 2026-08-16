# Design-Anforderungen – Kremer u. Grieb Schlosserei

## Nische & Design-Gefühl
- Branche/Nische: Schlosserei / Metallbau (Handwerk)
- Gewünschte Wirkung (3–5 Adjektive): solide, vertrauenswürdig, präzise, robust, klar

## Empfehlung aus ui-ux-pro-max
- Pattern/Produkt-Muster: Hero + Features (Leistungen) + CTA — bewährtes Einseiter-Schema für lokale Handwerksbetriebe (`engine/scripts/search.py --design-system`)
- Style: Basis „Swiss Modernism 2.0" (Grid, klare Hierarchie, rational) kombiniert mit der Branchenpalette „Construction/Architecture" (Industrial Grey + Safety Orange, `engine/data/colors.csv` Eintrag Nr. 51) — passender für einen Metallbaubetrieb als die automatisch vorgeschlagenen Styles „Glassmorphism"/„Kinetic Brutalism", die zu verspielt/tech-lastig für einen traditionsreichen Schlosser wirken
- Anti-Patterns (vermeiden): verspielte Formen/Pastelltöne, übertriebene Animationen, Glassmorphism-Blur (wirkt zu SaaS-artig, nicht handwerklich), Stockfoto-Ästhetik ohne Bezug zum Betrieb, erfundene Kundenstimmen/Siegel

## Farbwelt
- **Primär:** Anthrazit/Stahlgrau `#1E293B` — Stabilität, Präzision, Metall-Anmutung
- **Sekundär:** Kühles Grau `#64748B` — neutral, technisch, für Sekundärtexte/Rahmen
- **Akzent/CTA:** Signalorange `#EA580C` — Warnfarbe aus dem Handwerksumfeld (Sicherheit/Signal), starker Blickfang für Anruf-CTAs
- **Hintergrund:** Sehr helles Grau/Weiß `#F8FAFC` — sauber, lässt Inhalte/Leistungen wirken
- **Neutral/Text:** Dunkelgrau `#334155` für Fließtext (gute Lesbarkeit auf hellem Grund)
- Begründung: entspricht der Nischen-Empfehlung „Handwerk/Kfz: solide, vertrauenswürdig, klar; Blau/Anthrazit + Signalakzent" sowie der Branchenpalette „Construction/Architecture" aus der Design-Engine

## Typografie
- **Heading-Font:** Lexend — geometrisch-technisch, gute Lesbarkeit, wirkt modern und präzise ohne verspielt zu sein
- **Body-Font:** Source Sans 3 — sehr gut lesbar, neutral, deutschsprachetauglich (Umlaute), professionell
- Begründung: Pairing „Corporate Trust" aus `typography.csv` (Mood: corporate, trustworthy, accessible, readable, professional) — passt zum Vertrauensanspruch eines Handwerksbetriebs besser als verspielte Display-Fonts

## Bildsprache & Layout
- Fotostil: da keine echten Fotos vorliegen, Verzicht auf Fotografie zugunsten von klaren SVG-Icons (Zaun, Tor, Treppe, Schweißen, Schutz) je Leistungskachel + einer großflächigen, abstrakten Metall-/Linien-Textur (per CSS/SVG, kein Stockfoto-Etikettenschwindel als „eigene Arbeit")
- Formen/Ecken: klare Kanten, leicht abgerundete Karten (kleiner Radius, 4–8px) für Seriosität ohne Kälte
- Dichte: mittel — genug Weißraum für Klarheit, aber informationsdicht genug für Leistungsübersicht
- Sektionsreihenfolge: Header/Nav → Hero (CTA) → Leistungen (Kachelraster mit Icons) → Über uns → Öffnungszeiten (Platzhalter) → Kontakt/Anfahrt (Karte) → Footer

## Beispiel-Websites (Orientierung)
1. Allgemeine Recherche zu Metallbau-/Schlosserei-Websites (`websuche: "Schlosserei Metallbau Website Design"`) zeigt: robustes, industrielles Design, Leistungsgalerie (Geländer/Treppen), klare Anfrage-CTAs, mobile-first — als Prinzip übernommen, keine konkrete Seite kopiert
2. Recherche zu Locksmith-/Metallbau-Websites international (Colorlib „Best Locksmith Website Examples") bestätigt: klare Service-Karten mit Icons, hoher Kontrast bei Kontaktinformationen, seriöse statt verspielte Farbwelt — als Prinzip übernommen

## Do / Don't für diese Nische
- Do: klare Leistungsübersicht mit Icons, Telefon-CTA durchgängig sichtbar, seriöse Farbwelt (Anthrazit/Grau + ein Signalakzent), gute Lesbarkeit, Karte mit Adresse
- Don't: keine erfundenen Fotos/Referenzprojekte, keine erfundenen Bewertungen/Sterne, keine verspielten Pastelltöne, keine übertriebene Tech-/SaaS-Ästhetik (Glassmorphism/Neon), kein Stockfoto-Handwerker als „unser Team"
