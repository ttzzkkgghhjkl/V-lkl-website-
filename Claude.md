# Projekt: Landingpage Rechtsanwalt Stephan Völkel

## Worum es geht

Nachbau der Landingpage von Könnecke Naujok (https://www.kanzlei-handelsrecht-ffm.de/)
für Rechtsanwalt Stephan Völkel, Bad Soden am Taunus.
Struktur, Layout und Conversion-Mechanik werden 1:1 übernommen, die Inhalte kommen
aus dem Bestand unter https://www.rechtsanwaelte-voelkel-kollegen.de/

**Alle inhaltlichen Details stehen in `BRIEFING.md`. Vor jeder Aufgabe lesen.**

Die Referenz ist ein proprietäres System der OMERGY GmbH. Es gibt kein Theme und
kein Template zum Übernehmen — der Nachbau ist Handarbeit.

**Auftragslage:** Die Seite ist bislang **nicht beauftragt**. Sie entsteht auf
eigene Initiative neben einem laufenden Projekt für den Sohn des Kanzleiinhabers
und soll ihm anschließend zum Kauf angeboten werden. Daraus folgt: Das Ergebnis
muss ohne Nachfragen beim Inhaber überzeugen, und alles, wofür wir noch keine
Freigabe haben (Foto, Titelangaben, Werbeaussagen), wird als solches markiert
statt stillschweigend gesetzt.

## Arbeitsweise

- **Erst planen, dann bauen.** Bei jeder neuen Aufgabe zuerst den Plan zeigen und
  auf Freigabe warten. Nicht ungefragt losbauen.
- Ein Schritt nach dem anderen, keine drei Sektionen gleichzeitig.
- Bei Unklarheiten nachfragen statt Annahmen treffen. Offene Punkte stehen in
  BRIEFING.md Abschnitt 6 und sind **nicht** eigenmächtig zu entscheiden.
- Keine Platzhaltertexte wie „Lorem ipsum" oder erfundene Inhalte. Wenn etwas
  fehlt, `TODO:` mit Beschreibung setzen und melden.
- Keine erfundenen Fakten über die Kanzlei. Zahlen, Titel, Qualifikationen und
  Rechtsgebiete ausschließlich aus BRIEFING.md.

## Designtreue — der wichtigste Punkt

Das Ergebnis soll **visuell identisch** zur Referenz sein, nicht „im Stil von".
Kein freies Nachempfinden, kein generisches Framework-Look, keine eigenen
Designideen. Wenn ein Wert unklar ist, wird er **im Referenz-CSS nachgeschlagen,
nicht geschätzt**.

Deshalb wird vor dem ersten Bauschritt der komplette Frontend-Code der Referenz
gespiegelt und ausgewertet. Aus dem CSS werden exakt übernommen:

- Farbwerte (Hex/RGB), inklusive Hover- und Fokuszustände
- Schriftarten, Herkunft der Fonts, Schnitte, Größen, Zeilenhöhen,
  Letter-Spacing, Font-Weights je Element
- Abstände: Paddings, Margins, Container-Breiten, Grid-/Flex-Setup, Gaps
- Breakpoints und was an jedem umbricht
- Border-Radien, Schatten, Rahmen, Übergänge, Animationsdauern
- Button- und Formularstyles
- Icons: Herkunft und Darstellung

Diese Werte kommen zuerst in eine zentrale Token-Datei (CSS Custom Properties),
erst danach wird die erste Sektion gebaut. Ziel ist, dass wir **nicht** Sektion für
Sektion nachträglich Abweichungen wegprompten müssen.

Wenn ein Detail im Code nicht auffindbar ist: melden, nicht erfinden.

**Vorrangregel:** Bei jedem Konflikt zwischen diesem Abschnitt und den
Konventionen weiter unten gewinnt die Designtreue. Die Konventionen gelten dort,
wo sie das visuelle Ergebnis nicht verändern. Betrifft konkret „Mobile first":
wenn die Referenz getrennte Desktop-/Mobile-Blöcke im DOM verwendet, bauen wir
das nach, statt es responsiv umzuschreiben.

Rechtlich sauber trennen: **Struktur und Optik** werden übernommen, **Texte**
werden neu geschrieben (siehe unten). Fremde Bilder und lizenzpflichtige
Schriften werden nicht mitgenommen, sondern ersetzt bzw. korrekt lizenziert.

## Texte

Die Formulierungen der Referenzseite sind urheberrechtlich geschützt.
Übernommen werden Struktur, Reihenfolge, Aufbau und Tonalität — **nicht der
Wortlaut**. Alle Texte werden neu geschrieben.

Ausnahme: kurze funktionale Beschriftungen (Buttons, Formularlabels, „Termine
innerhalb von 24h") sind unkritisch.

## Aktueller Stand

- [x] Referenz analysiert, Sektionsplan steht (BRIEFING.md Abschnitt 2)
- [x] Inhalte des Bestands gesichtet
- [ ] Referenzseite lokal gespiegelt, Code analysiert (BRIEFING.md Abschnitt 8)
- [ ] Stack entschieden
- [ ] Projektstruktur angelegt
- [ ] Sektionen gebaut

Nächster Schritt: **Abschnitt 8 des Briefings** — beide Seiten spiegeln, dann den
Code der Referenz auswerten und die dort gelisteten sechs Fragen beantworten.
Falls die Domain durch die Netzwerk-Allowlist blockiert wird (`403
host_not_allowed`), melden statt umgehen.

## Stack

Noch nicht entschieden. Tendenz: statisches HTML/CSS mit schlankem Vanilla-JS
plus Formmailer, weil es sich um eine einzelne Landingpage handelt.
Vor der Entscheidung erst den Code der Referenz ansehen.

Sobald entschieden, hier eintragen.

## Konventionen

- Sprache im Frontend: Deutsch, Ansprache „Sie"
- Kommentare und Commit-Messages: Deutsch
- Mobile first — die Referenz trennt Desktop- und Mobile-Blöcke im DOM,
  ob wir das übernehmen, wird nach der Code-Analyse entschieden
- Keine Tracking-Skripte ohne ausdrückliche Freigabe. Die Google-Analytics-ID
  des Bestands (`G-RTBS5Q7HCW`) wird **nicht** blind übernommen.
- Barrierefreiheit mitdenken: semantisches HTML, Alt-Texte, Kontraste,
  Tastaturbedienbarkeit. Die Zielgruppe ist teils älter, im Bestand gibt es
  sogar einen Hausbesuchs-Service für nicht mobile Mandanten.
- Performance: Bilder in modernen Formaten, Lazyload, keine schweren Libraries

## Ordnerstruktur

```
/referenz     gespiegelte Referenzseite, nur Analyse, wird nie deployed
/bestand      gespiegelte Altseite von Völkel, Inhaltsquelle
/src          der eigentliche Nachbau
/assets       Bilder, Icons, Schriften
BRIEFING.md   vollständiges Projektbriefing
CLAUDE.md     diese Datei
```

`/referenz` und `/bestand` gehören in `.gitignore`, sobald sie existieren —
fremde Inhalte werden nicht mitversioniert.

## Nicht vergessen

- Fachanwaltstitel Erbrecht und die 24-Stunden-Zusage vor Livegang schriftlich
  vom Mandanten bestätigen lassen
- Auf der Live-Seite des Bestands ist ein Logout-Link zum IONOS-Editor sichtbar —
  prüfen, ob dort eine Session offen liegt
- Redirects für die alten URLs planen

