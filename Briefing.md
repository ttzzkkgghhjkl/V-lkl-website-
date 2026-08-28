# Projekt-Briefing: Landingpage Rechtsanwalt Stephan Völkel

Nachbau der Referenz-Landingpage von Könnecke Naujok (Frankfurt) für Rechtsanwalt
Stephan Völkel (Bad Soden am Taunus). Struktur, Layout und Conversion-Logik 1:1,
Inhalte aus dem Bestand von Völkel.

Stand: 28.08.2026

---

## 0. Die beiden Seiten

**Referenz (Vorbild für Aufbau und Optik)**
https://www.kanzlei-handelsrecht-ffm.de/
Könnecke Naujok Rechtsanwälte Partnerschaftsgesellschaft mbB, Westendstraße 28,
60325 Frankfurt am Main, Tel. (069) 98 93 98 05

**Bestand (Quelle aller Inhalte, wird ersetzt)**
https://www.rechtsanwaelte-voelkel-kollegen.de/
Rechtsanwalt Stephan Völkel, Zum Quellenpark 7, 65812 Bad Soden am Taunus

Alle Unterseiten des Bestands:
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsanwalt-stephan-völkel/
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsgebiete/
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsgebiete/arbeitsrecht/
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsgebiete/erbrecht/
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsgebiete/familienrecht-scheidung/
- https://www.rechtsanwaelte-voelkel-kollegen.de/rechtsgebiete/strafrecht/
- https://www.rechtsanwaelte-voelkel-kollegen.de/service-für-nicht-mobile-menschen-hausbesuche-des-anwalts/
- https://www.rechtsanwaelte-voelkel-kollegen.de/formulare/
- https://www.rechtsanwaelte-voelkel-kollegen.de/vorsorgevollmacht-patientenverfügung/
- https://www.rechtsanwaelte-voelkel-kollegen.de/praxistipp/
- https://www.rechtsanwaelte-voelkel-kollegen.de/telefonzeiten/
- https://www.rechtsanwaelte-voelkel-kollegen.de/kontakt/
- https://www.rechtsanwaelte-voelkel-kollegen.de/gebühren/
- https://www.rechtsanwaelte-voelkel-kollegen.de/qualifikation-fortbildung/
- https://www.rechtsanwaelte-voelkel-kollegen.de/links/
- https://www.rechtsanwaelte-voelkel-kollegen.de/impressum/
- https://www.rechtsanwaelte-voelkel-kollegen.de/datenschutz/
- https://www.rechtsanwaelte-voelkel-kollegen.de/sitemap/

Bislang inhaltlich ausgelesen: Startseite, Anwaltsprofil, Rechtsgebiete
(Übersicht), Telefonzeiten, Gebühren, Hausbesuche, Impressum.
**Noch offen:** die vier Rechtsgebiets-Unterseiten, Formulare, Vorsorgevollmacht,
Praxistipp, Qualifikation/Fortbildung, Kontakt, Datenschutz.

---

## 1. Worauf die Referenzseite technisch basiert

Kein Standard-CMS. Die Seite kommt aus einem **proprietären Landingpage-System
der OMERGY GmbH** (bis 15.09.2023 adzLocal GmbH), Lippeltstr. 1, 20097 Hamburg,
HRB 110466 Hamburg. OMERGY ist auf Performance-Marketing für Anwaltskanzleien
spezialisiert, das Produkt heißt schlicht „Landingpage" und wird als Paket mit
Google-Ads-Kampagne, Telefonservice und Betreuungsflatrate verkauft.

Belege im Quelltext:
- Footer: „Webdesign & Onlinemarketing von OMERGY", https://www.omergy.de/
- Asset-Host `renderer.omergy.de` — deutet auf einen zentralen Renderer, der aus
  einem Kunden-Datensatz statische Seiten erzeugt (Kunden-ID im Pfad: `1497267`)
- Bild-CDN `images.omergy.de` mit Cloudinary-Transformations-Syntax,
  Cloudinary-Account `adzlocal-gmbh`

**Konsequenz:** Es gibt kein Theme, kein Template und kein Plugin, das man kaufen
oder klonen könnte. Der 1:1-Nachbau ist Handarbeit. Wir bauen die Optik und die
Conversion-Mechanik nach, nicht das System dahinter. Das ist eher ein Vorteil —
wir sind bei Stack und Hosting frei.

Vor Baubeginn im Terminal zu verifizieren (siehe Abschnitt 8): Server-Header,
Generator-Meta, ob ein JS-Framework geladen wird.

### Beobachtete Umsetzungstechniken der Referenz

- **Hero-Aufhellung nicht per CSS-Overlay, sondern in die Bildtransformation
  gebacken:** `co_rgb:ffffff,e_colorize:80` — Weiß-Overlay mit 80 % Stärke
- **Fester Bildausschnitt serverseitig:** `c_crop` mit expliziten x/y/w/h-Werten,
  danach `c_fill,g_center,f_auto`
- **Lazyload mit Mini-Placeholder:** erste Auslieferung mit `w_50`, dann Swap auf
  die volle Auflösung
- **Getrennte Desktop-/Mobile-DOM-Blöcke:** jeder Hero-Textblock steht doppelt im
  Markup und wird per CSS ein-/ausgeblendet, statt ein Block responsiv umzubrechen
- **Zwei komplette Hero-Sektionen** mit unterschiedlichen Bullets und
  unterschiedlichen Trust-Punkten (Variante A: „Zusätzlich Qualifikation als
  Steuerberater" / Variante B: „Besondere Expertise im Immobiliensektor",
  „Expertise von mehreren Anwälten"). Vermutlich kampagnenabhängige Ausspielung
  über die Google-Ads-Parameter. **Muss im Code geprüft werden** — sonst bauen wir
  eine Variante nach, die dort nur eine von zweien ist.
- `<meta name="format-detection" content="telephone=no">`, alle Nummern manuell
  als `tel:`-Links
- Cookie-Banner mit granularer Auswahl (Alle ablehnen / Auswahl speichern /
  Weitere Infos / Verstanden)
- Bildquellen sind Unsplash-Fotos (Dateinamen erhalten:
  `frankfurt-photographer-4Nc8fXLuGN4`, `justus-menke-FbZpIuLZja8`,
  `raja-sen-nN863yJtfTo`) plus Stockmaterial für die Leistungskacheln

---

## 2. Sektionsplan — Referenzstruktur mit Völkel-Inhalten

### Sektion 1 — Sticky Header
- Referenz: Logo links, Telefonnummer rechts als Click-to-Call, Nummer doppelt im
  DOM (Desktop/Mobile)
- Völkel: Wortmarke „Rechtsanwalt Stephan Völkel" (kein Logo vorhanden — muss
  gesetzt oder gestaltet werden)
- Telefon: `tel:+496196600810`, Anzeige „06196 600810"

### Sektion 2 — Hero (Bild, H1, 3 Bullets, Fließtext, CTA)
- H1: „Anwaltskanzlei für Arbeits-, Familien- und Erbrecht in Bad Soden am Taunus"
  (Referenz-H1 zum Vergleich: „Anwaltskanzlei für Handels- und Gesellschaftsrecht
  in Frankfurt am Main")
- Bullets (Referenz hat exakt 3, fett gesetzt):
  - Kündigungsschutz & Abfindung im Arbeitsrecht
  - Scheidung, Unterhalt & Sorgerecht
  - Testament, Erbfolge & Vermögensübertragung
- Fließtext-Bausteine aus dem Bestand:
  - kleine, aber feine Kanzlei, beratend und vor Gericht tätig
  - Mandanten: Privatpersonen, Handwerksbetriebe, Gesellschaften mit bis zu
    400 Mitarbeitern
  - bundesweit tätig, Schwerpunkt Rhein-Main-Gebiet
  - internationale Mandanten willkommen, Beratung auf Englisch
  - außergerichtliche Beratung und gerichtliche Vertretung
  - Netzwerk zu ausgewählten Rechtsanwälten für angrenzende Themen
- CTA wie Referenz: „Rufen Sie uns gerne an!" + Telefonnummer

### Sektion 3 — Anwalts-Badge im Hero
- Referenz: rundes Portraitfoto 64×64, darunter „Rechtsanwalt", Name, dann
  4 Trust-Punkte mit Icon, dann Telefon-Button und Textlink „oder Rückruf per
  E-Mail anfordern"
- Völkel:
  - Foto: https://www.rechtsanwaelte-voelkel-kollegen.de/s/cc_images/cache_2418417674.jpg?t=1612785482
  - „Rechtsanwalt / Stephan Völkel / Fachanwalt für Arbeitsrecht"
  - Trust-Punkte (4, analog zur Referenz):
    1. Termine innerhalb von 24h
    2. Über 30 Jahre Berufserfahrung
    3. Fachanwalt für Arbeitsrecht und für Erbrecht
    4. Erreichbar Mo–Fr von 7 bis 19 Uhr

### Sektion 4 — Zweite Hero-Variante
- Existiert in der Referenz als kompletter zweiter Block. Erst nach Code-Analyse
  entscheiden, ob wir sie nachbauen (A/B, kampagnenabhängig) oder weglassen.

### Sektion 5 — „Welches Anliegen haben Sie?" (Leistungskacheln)
Referenz: 3 Kacheln, je Bild oben, H3, darunter 2–4 Stichpunkte.

**Feste Vorgabe: vier Kacheln.** Völkel hat vier Rechtsgebiete, die alle sichtbar
sein müssen. Das ist eine bewusste, nicht verhandelbare Abweichung von der
Referenz und der einzige Punkt, an dem die Struktur abweicht.

Dabei gilt: Die **Kachel selbst bleibt exakt wie in der Referenz** — Bildformat,
Überschriftenstil, Stichpunktdarstellung, Innenabstände, Radien, Schatten,
Hover-Verhalten. Geändert wird ausschließlich die Spaltenzahl des Grids.

Wie das Grid gelöst wird, ist **nach der CSS-Analyse zu entscheiden**, nicht
vorher zu raten. Zwei Kandidaten: 2×2 auf Desktop, oder vier in einer Reihe mit
angepassten Breakpoints. Ausschlaggebend ist, welche Variante der Referenzoptik
näher bleibt. Vorschlag zur Freigabe vorlegen, bevor gebaut wird.

- **Arbeitsrecht** — Kündigungsschutzklage, Abfindungsverhandlung,
  Aufhebungsvertrag, Zeugnis
- **Familienrecht** — Scheidung, Unterhalt, Sorgerecht, Zugewinnausgleich
- **Erbrecht** — Testamentsgestaltung inkl. steuerlicher Aspekte,
  Vermögensübertragung zu Lebzeiten, Pflichtteil, Erbauseinandersetzung
- **Strafrecht & allgemeines Zivilrecht** — Strafverteidigung, Ermittlungs-
  verfahren, allgemeine zivilrechtliche Streitigkeiten

Ergänzende Aussage aus dem Bestand, passt unter die Kacheln: „Sie können mit jedem
rechtlichen Problem auf uns zukommen. Wenn wir die Rechtsmaterie nicht selbst
bearbeiten, empfehlen wir einen kompetenten Partner." (umformulieren, nicht 1:1)

### Sektion 6 — 3-Schritte-Ablauf
Referenz: nummerierte Kreise 1/2/3 mit Überschrift und einem Satz.
- **1 Kontaktaufnahme** — unverbindlich anrufen oder E-Mail schreiben,
  telefonisch erreichbar Mo–Fr 7–19 Uhr
- **2 Terminvereinbarung** — Termin innerhalb von 24 Stunden, auf Wunsch auch
  außerhalb der Telefonzeiten, bei Bedarf als Hausbesuch
- **3 Beratungsgespräch** — gemeinsame Strategie, Kosten werden im ersten
  Gespräch offen besprochen

### Sektion 7 — CTA-Banner mit aufgehelltem Hintergrundbild
- Referenz: „Direkt anrufen & beraten lassen" / „Termine innerhalb von 24h" /
  Telefonnummer / „Jederzeit Rückruf per E-Mail anfordern"
- Für Völkel identisch übernehmen, Nummer tauschen

### Sektion 8 — „Nähere Infos zu unserer Kanzlei"
Referenz: großes Portraitfoto links, Bildunterschrift kursiv (Name, Rechtsanwalt),
rechts drei Textblöcke mit Zwischenüberschrift, darunter Verbandslogo und drei
weitere Trust-Bullets.

Textblock 1 — **Fachspezifische Kompetenz**
- Fachanwalt für Arbeitsrecht (2004), Fachanwalt für Erbrecht (2005)
- Wissenschaftlicher Mitarbeiter am Lehrstuhl für Arbeitsrecht,
  Justus-Liebig-Universität Gießen (während des Referendariats)
- Notariatslehrgang 1999, Notariatsverwalter 1999/2000, Notariatsvertreter
  1994–1999
- Seit Mai 1994 als Rechtsanwalt zugelassen

Textblock 2 — **Persönliche Beratung**
Basis ist das Selbstverständnis aus dem Anwaltsprofil (umformulieren):
Mandant steht im Vordergrund, Ehrlichkeit über die Erfolgsaussichten, bewusst mehr
Zeit für Besprechungen, um gemeinsam eine Strategie zu entwickeln.

Textblock 3 — **Transparente Kosten**
- Abrechnung in der Regel auf Stundenhonorarbasis, teils Pauschalhonorar
- Frage nach der Kostenhöhe ist immer kostenfrei
- Grundlage RVG
- kostenfreie Deckungsanfrage bei bestehender Rechtsschutzversicherung
- Beratungshilfeschein über das Amtsgericht, PKH/VKH-Anträge möglich

Siegel / Trust-Bullets (ersetzen das DAV-Logo der Referenz):
- **DAV** — Deutscher Anwaltverein
- **DVEV** — Deutsche Vereinigung für Erbrecht und Vermögensnachfolge e.V.
- Hausbesuche für ältere oder nicht mobile Mandanten
- Beratung auf Englisch
- Kombination aus Rechtsberatung und steuerlicher Betrachtung im Erbrecht

### Sektion 9 — Google-Bewertungen (Neuerung gegenüber der Referenz)
Die Referenz hat keinen Review-Block. Völkel hat mit 4,9 aus 25 einen besseren
Trust-Anker, als die Referenz überhaupt anzubieten hat. Siehe Abschnitt 4.
Platzierung: zwischen Sektion 8 und 10.

### Sektion 10 — „So erreichen Sie uns"
- Rechtsanwalt Stephan Völkel, Zum Quellenpark 7, 65812 Bad Soden am Taunus
- Telefon 06196 600810 · Telefax 06196 27351
- E-Mail: **klärungsbedürftig**, siehe Abschnitt 6
- Telefonzeiten Mo–Fr 7–19 Uhr; Termine auch außerhalb nach Absprache
- ÖPNV: Bushaltestelle „Kurpark" ca. 100–150 m, Bahnhof Bad Soden (Taunus),
  S3 Richtung Frankfurt, ca. 250 m Luftlinie (Fußwegzeiten vor Livegang real prüfen)
- Parken: entfällt, keine Angaben vorhanden
- Kartenausschnitt: Koordinaten 50.1437178, 8.5002236
- **Warnhinweis aus dem Bestand unbedingt übernehmen:** Bei ablaufenden Fristen
  bitte nur telefonisch oder persönlich Kontakt aufnehmen; die Fristenkontrolle
  beginnt erst mit ausdrücklicher Mandatsübernahme.

### Sektion 11 — Rückruf-Formular
Referenz-Felder: Name, E-Mail, Telefon (optional), Nachricht, Hinweis auf
SSL-Verschlüsselung und Datenschutzerklärung, Button „Rückrufbitte absenden".
1:1 übernehmen. Versandweg (Mail, Formmailer, Backend) ist eine Stack-Entscheidung.

### Sektion 12 — Footer
Kanzleiname, Impressum, Datenschutz. Der Credit-Link auf OMERGY entfällt
selbstverständlich.

### Sektion 13 — Cookie-Banner
Granulare Zustimmung analog Referenz.

---

## 3. Impressumsdaten (vollständig vorhanden)

- Rechtsanwalt Stephan Völkel, Zum Quellenpark 7, 65812 Bad Soden am Taunus
- Telefon +49 6196 600810, Telefax +49 6196 27351
- Umsatzsteuer-ID: 181 351 248 (DE-Präfix wird nachträglich geklärt, so übernehmen)
- Berufsbezeichnung: Rechtsanwalt (verliehen in der Bundesrepublik Deutschland)
- Zuständige Kammer: Rechtsanwaltskammer Frankfurt am Main
- Berufshaftpflichtversicherung: Allianz
- Berufsrechtliche Regelungen: RVG, BRAO, BORA, FAO, CCBE-Berufsregeln
- Verweis auf die Bundesrechtsanwaltskammer: https://www.brak.de, Rubrik Berufsrecht
- Haftungsausschluss und Linkhaftung sind im Bestand ausformuliert vorhanden

---

## 4. Google-Bewertungen

- Profil: **Rechtsanwalt Stephan Völkel**, Zum Quellenpark 7
- **4,9 Sterne bei 25 Bewertungen**
- Google Place ID: `ChIJR4lrbummvUcR7BWDulh31b8`
- Koordinaten: 50.1437178, 8.5002236
- Im Profil hinterlegte Öffnungszeiten Mo–Fr 7:00–19:00, Sa/So geschlossen —
  deckt sich mit den Telefonzeiten der Website
- Auf der bestehenden Website ist das Profil **nirgends verlinkt**. Das ist die
  größte ungenutzte Ressource des Mandanten.
- Inhaltlich decken die Rezensionen exakt unsere geplanten Kacheln ab:
  Abfindungsverhandlung im Arbeitsrecht, Scheidung, Immobilienübertragung an die
  Kinder ohne Schenkungsteuer, eingestelltes Strafverfahren, Testament und
  Vorsorgevollmacht
- Umsetzung: echtes Google-Reviews-Widget oder statisch gepflegte Zitate plus
  Verlinkung auf das Profil. Bei statischer Einbindung Namen und Datum korrekt
  übernehmen und die Quelle nennen.

Nicht verwenden:
- 11880.com — Altbestand als „Völkel & Kvas", 3,71 aus 7 Bewertungen
- Cylex, Trustlocal, Infobel, anwalt-suchservice, rechtecheck — Scraper-Einträge
  ohne eigenen Wert, teils mit falschen Daten

---

## 5. Fehlende Assets

- **Logo / Wortmarke** — existiert nicht, muss gestaltet werden
- **Aktuelles Portraitfoto** — vorhandenes stammt aus 2021, Auflösung für einen
  großen Hero-Einsatz vermutlich zu gering
- **Kanzleifoto / Außenaufnahme** — nicht vorhanden
- **Hero-Hintergrundbild** — die Referenz nutzt ein Frankfurt-Skyline-Motiv von
  Unsplash. Für Völkel bietet sich Bad Soden an; im Bestand liegt bereits ein Foto
  „Solebrunnen mit Sodenia vor dem Hundertwasserhaus" (cache_2421253592.jpg),
  Auflösung und Nutzungsrechte prüfen
- **Bilder für die Leistungskacheln** — 4 Stück, Stockmaterial
- Das aktuelle Headerbild `1001-emotionheader.jpg` ist ein IONOS-Standardmotiv und
  wird nicht übernommen

---

## 6. Offene Punkte für den Mandanten

1. **E-Mail-Adresse.** Drei widersprüchliche Angaben im Umlauf:
   `info@rechtsanwaelte-voelkel-kollegen.de` (Anzeigetext im Impressum), der
   Mailto-Link dahinter zeigt aber auf die alte Domain
   `info@rechtsanwaelte-voelkel-kvas.de`, und auf rechtecheck.de steht
   `voelkel13@yahoo.de`. Verbindliche Klärung nötig.
2. **Kanzleiname.** Domain und Titel sagen „& Kollegen", es gibt aber keine
   Kollegen. Entweder Namen anpassen oder Domain beibehalten und im Text
   konsequent Ich-Form verwenden. Die Referenz spricht durchgehend „wir" —
   bei einem Einzelanwalt ist das eine bewusste Entscheidung.
3. **Fachanwalt für Erbrecht** und **Termine innerhalb von 24h** vor Livegang
   einmal schriftlich bestätigen lassen. Beides sind berufsrechtlich relevante
   Werbeaussagen, für die der Mandant geradesteht.
4. Sollen die Bestandsseiten Formulare, Praxistipp, Vorsorgevollmacht und Links
   erhalten bleiben oder entfallen?
5. Domain: bleibt `rechtsanwaelte-voelkel-kollegen.de` oder Umzug?
6. Hosting und Postfach liegen aktuell bei IONOS (MyWebsite). Zugänge klären.

---

## 7. Technische Rahmenbedingungen des Bestands

- CMS: IONOS MyWebsite (`meta-generator: IONOS MyWebsite`), Editor unter
  `107.sb.mywebsite-editor.com`, Site-ID 604162319
- **Auf der Live-Seite ist ein Logout-Link sichtbar** — das deutet auf eine
  eingeloggte Session oder auf ein Leck im Template. Vor Übergabe prüfen.
- Google Analytics Measurement ID im Quelltext sichtbar: `G-RTBS5Q7HCW`
- Kein SEO-Fundament vorhanden, das erhalten werden müsste. Redirects sind
  trotzdem zu planen, damit die bestehenden URLs nicht ins Leere laufen.

---

## 8. Nächster Schritt im Terminal

Der Container hier hat eine Domain-Allowlist, `kanzlei-handelsrecht-ffm.de` steht
nicht drauf (`403 host_not_allowed`). Lokal greift das nicht. Zuerst also die
Referenz vollständig sichern:

```bash
mkdir -p ~/projekte/voelkel/referenz && cd ~/projekte/voelkel/referenz

# Header und Generator prüfen
curl -sI -A "Mozilla/5.0" https://www.kanzlei-handelsrecht-ffm.de/

# Seite komplett spiegeln inkl. CSS, JS, Bilder
wget --mirror --page-requisites --convert-links --adjust-extension \
     --no-parent --user-agent="Mozilla/5.0" \
     https://www.kanzlei-handelsrecht-ffm.de/

# Zweite Variante mit Kampagnenparametern ziehen und gegen die erste diffen
curl -sA "Mozilla/5.0" "https://www.kanzlei-handelsrecht-ffm.de/?gad_source=1&gad_campaignid=21017748650" \
     -o variante-b.html
```

Danach zu klären, bevor gebaut wird:
- Läuft ein JS-Framework oder ist es statisches HTML mit etwas Vanilla-JS?
- Wie werden die beiden Hero-Varianten umgeschaltet?
- Wie sind die Breakpoints gesetzt, an denen Desktop- und Mobile-Blöcke tauschen?
- Welche Schriften werden geladen, von wo?
- Wie ist das Formular verdrahtet, wohin geht der Request?
- Welches Cookie-Consent-Tool ist im Einsatz?

Und die Bestandsseiten von Völkel, die noch nicht ausgelesen sind:

```bash
mkdir -p ~/projekte/voelkel/bestand && cd ~/projekte/voelkel/bestand
wget --mirror --page-requisites --convert-links --adjust-extension \
     --no-parent --user-agent="Mozilla/5.0" \
     https://www.rechtsanwaelte-voelkel-kollegen.de/
```

Offene Stack-Entscheidung: statisches HTML/CSS mit etwas JS, oder ein Framework.
Für eine einzelne Landingpage mit Formular spricht viel für statisch plus einen
schlanken Formmailer.
