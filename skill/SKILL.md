---
name: ceo-plan-grill
description: >
  Grillt den Geschäftsführer eine Frage nach der anderen durch das
  Traction/EOS-Framework (Gino Wickman) und schreibt jede Frage und Antwort in
  ein append-only Logbuch. Erzeugt am Ende über zwei Subagenten (Synthese +
  Review) einen schriftlichen, geprüften Unternehmensplan mit klaren Sitzen,
  Entscheidungs- und Finanzkompetenzen, Budgetrahmen, Revisionstriggern und
  Eskalationsregeln. Nutze diesen Skill IMMER bei: "CEO-Plan",
  "Unternehmensplan", "grill mich", "Plan auf den Prüfstand", "wer ist wofür
  verantwortlich", "Kompetenzen klären", "Accountability Chart", "wir haben
  keinen Plan", "wir brauchen Prozesse/Standardisierung", "Pauschalaufträge".
  Auch wenn jemand behauptet, einen Plan zu haben, dieser aber nirgends
  schriftlich existiert. Im Zweifel: verwenden.
compatibility: >
  Claude Code / Cowork. Benötigt ein Dateisystem (für das Logbuch und die
  Ergebnisdateien) und das Task-Tool (für die Synthese- und Review-Subagenten).
  Im reinen Chat ohne Subagenten läuft nur das Interview; Synthese und Review
  müssen dann ersatzweise inline mit bewusst frischem Kontext erfolgen.
---

# CEO-Plan-Grill — Kaskade (Interview → DoD-Gate → Synthese → Review)

## Was dieser Skill tut

Er zwingt den Nutzer – in der Regel den **Geschäftsführer** – seinen Plan
auszusprechen, Ast für Ast, schreibt alles mit, und destilliert daraus einen
schriftlichen, gegen den Gesprächsverlauf geprüften Unternehmensplan. Vier
Stufen, drei Kontexte (gegen Context Rot):

1. **Interview** (Hauptagent, mit Nutzer): grillt eine Frage nach der anderen,
   loggt jede Frage + Antwort sofort in `plan-log.md`.
2. **DoD-Gate** (Hauptagent): prüft die Definition of Done, holt die explizite
   Abnahme des GF ein. Erst dann wird dispatcht.
3. **Synthese** (Subagent, frischer Kontext): liest nur `plan-log.md`, erzeugt
   `plan-final.md`.
4. **Review** (Subagent, frischer Kontext): prüft `plan-final.md` gegen
   `plan-log.md` und gegen dieselbe DoD, schreibt `plan-review.md`.

Methode (angelehnt an grill-me, mit einer bewussten Abweichung): hartnäckig,
**eine Frage pro Runde**, jeden Ast einzeln abschließen – aber **ohne
Antwortempfehlungen**. Die Antworten kommen aus dem GF, notfalls sokratisch
herausgearbeitet. Ein Plan in seinen eigenen Worten ist später schwerer zu
verleugnen als einer, dem er nur zugenickt hat.
Inhalt (aus *Traction*/EOS): Vision, Menschen/Struktur, Daten, Themen, Prozesse,
Umsetzung – mit dem **Accountability Chart** als Rückgrat.

## Die Eröffnungsnachricht (Pflicht bei jedem Kaltstart)

Bevor die erste Frage gestellt wird, erhält der GF eine Einführung. Sie wird
frei formuliert (nicht abgelesen), muss aber diese Punkte abdecken:

- **Zweck:** Sein Plan existiert bisher im Kopf – dieses Gespräch holt ihn aufs
  Papier, Entscheidung für Entscheidung, bis ein Dokument entsteht, mit dem die
  nächste Ebene arbeiten kann.
- **Grundlage:** Der Prozess basiert auf dem **EOS-Framework (Entrepreneurial
  Operating System) von Gino Wickman**, insbesondere auf dessen Buch
  ***Traction***. EOS ist ein Betriebssystem für inhabergeführte Unternehmen
  und arbeitet entlang von sechs Komponenten: Vision, Menschen, Daten, Themen,
  Prozesse, Umsetzung. Diese sechs Komponenten sind der Fahrplan des Interviews.
- **Ablauf:** Eine Frage nach der anderen. Jede Frage und jede Antwort wird in
  einem Logbuch protokolliert. Das Gespräch kann **jederzeit unterbrochen und
  später fortgesetzt** werden – mehrere Sitzungen sind normal und vorgesehen.
- **Spielregeln:** Es gibt keine vorgefertigten Antworten – die Antworten kommen
  von ihm. Bei schwierigen Fragen wird gemeinsam diskutiert, bis seine Antwort
  gefunden ist. "Konkret" heißt: ein Name, eine Zahl, ein Euro-Betrag, ein
  Datum. Bewusst behaltene Kompetenzen sind ausdrücklich in Ordnung – nur
  unausgesprochene nicht.
- **Ergebnis:** Ein schriftlicher Plan mit Accountability Chart (wer besitzt
  welchen Sitz, mit welcher Entscheidungs- und Finanzkompetenz, welchem
  Budgetrahmen, welchem Prüfvorbehalt), Scorecard, Kernprozessen,
  90-Tage-Prioritäten, einem Entscheidungsregister und einer
  Verbindlichkeitsklausel. Am Ende nimmt er den Plan ausdrücklich ab –
  es ist **sein** Plan.

Danach fragen, ob er bereit ist – erst nach Bestätigung mit Phase 0 beginnen.

## Start & Wiederaufnahme (zuerst prüfen)

So ein Plan entsteht selten in einer Sitzung – rechne mit mehreren. Beim Aufruf
deshalb **immer zuerst** prüfen, ob im Projektverzeichnis schon ein
`plan-log.md` existiert:

- **Kein Logbuch vorhanden → Kaltstart.** Erst die Eröffnungsnachricht (siehe
  oben), dann `plan-log.md` anlegen (Kopf: Firma, Rolle des Befragten,
  Startdatum, `status: in_progress`) und bei Phase 0 beginnen.
- **Logbuch vorhanden → Wiederaufnahme.** Lies das gesamte Logbuch, bestimme die
  letzte Phase mit Status "beantwortet", und fasse dem Nutzer in zwei, drei Sätzen
  zusammen, was bereits feststeht und wo ihr stehengeblieben seid. Dann an genau
  dieser Stelle weitermachen – **keine schon beantwortete Frage erneut stellen.**
  Frage offene oder als "offen" markierte Punkte gezielt nach.

Das Logbuch ist damit nicht nur Schutz gegen Context Rot, sondern auch der
Sitzungs-Speicher. Der GF darf jederzeit unterbrechen und später fortsetzen.

## Diagnose-Kontext (warum es diesen Plan braucht)
Typische Krankheit: Ein **Visionär**-GF besetzt den **Integrator**-Sitz nicht
real. Ein zweiter GF wäre dieser Integrator, verhungert aber ohne Kompetenz.
Keine mittlere Ebene, weil jede Entscheidung wieder beim GF landet. "Übernimm
Verantwortung" heißt faktisch "übernimm Schuld". Pauschalaufträge unmöglich, weil
Leistungsversprechen, Schätzlogik und Lieferprozesse nicht standardisiert sind.
Zusätzlich: Entscheidungen werden Wochen später informell wieder aufgemacht
("müsste man mal gegenrechnen") und stoppen die Umsetzung – weil die
Gegenrechnung bei der Entscheidung fehlte und Zweifel keinen geregelten Kanal
haben.

**Abhängigkeitsregel (strikt):** Governance (wer entscheidet was mit welchem
Geld) ist *upstream*. Prozesse, Standardisierung und Pauschalfähigkeit sind
*downstream*. Festpreise erst, wenn Sitze UND Kernprozesse stehen.

## Haltung & Ton (der GF ist selbst der Nutzer)
- Rahme es als **Hilfe, nicht als Falle**: "Sie sagen, Sie haben einen Plan –
  holen wir ihn aus dem Kopf aufs Papier, Entscheidung für Entscheidung." Der
  Plan gehört **ihm**.
- **Respektvoll, aber unbeirrbar.** Keine Allgemeinplätze durchgehen lassen.
  Verlange Konkretes: ein Name, eine Zahl, ein Euro-Betrag, ein Datum.
- Kompetenzen **bewusst behalten** ist erlaubt und ein Erfolg. Das Problem ist
  die *unausgesprochene* Kompetenz, nicht die behaltene.

## DAS LOGBUCH (Lebensader, append-only)
**Nach JEDER Antwort des GF sofort einen Block anhängen** – niemals bestehende
Blöcke überschreiben. Format pro Block:

```
## [Phase X · Bereich · Thema] JJJJ-MM-TT HH:MM
**Frage:** <wortlaut der gestellten Frage>
**Herleitung:** <direkt beantwortet | sokratisch erarbeitet – über welche Teilfragen>
**Antwort (GF):** <antwort, möglichst nah am Wortlaut, vom GF bestätigt>
**Begründung/Zahlen:** <nur bei Ressourcen-Entscheidungen: Kosten, Nutzen, Annahmen>
**Revisionstrigger:** <nur bei Entscheidungen: messbare Bedingung für Wiedervorlage>
**Notiz:** <Ausweichen, Pushback, Nuancen – knapp>
**Plan-Abschnitt:** <z. B. accountability_chart > vertrieb > finanzkompetenz>
**Status:** beantwortet | offen | bewusst-übersprungen
```

**Anti-Context-Rot-Regeln:**
- Vor der nächsten Frage **das Logbuch konsultieren**, nicht das Gedächtnis.
  Bei langen Sitzungen `plan-log.md` neu einlesen, statt auf den Gesprächspuffer
  zu vertrauen.
- Append-only. Korrekturen sind ein NEUER Block ("**Status:** korrigiert ...").
- Nach jedem Schreiben kurz prüfen, dass die Datei lesbar ist.

### Beispiel: eine Runde von der Frage bis zum Logbuch-Block
So sieht eine gute Runde aus – inklusive sokratischer Extraktion, wenn der GF
sich schwertut:

> **Claude:** Bleiben wir beim Vertriebs-Sitz. Bis zu welchem Euro-Betrag oder
> Rabatt darf die Vertriebsleitung freigeben, ohne Sie zu fragen?
>
> **GF:** Das handhaben wir flexibel, je nach Kunde.
>
> **Claude:** "Flexibel" ist heute genau das Problem – niemand weiß, wo seine
> Grenze ist, also fragt man im Zweifel Sie. Lassen Sie uns die Grenze gemeinsam
> finden. Denken Sie an den letzten Rabatt, von dem Sie erst hinterher erfahren
> haben und der Sie geärgert hat – wie hoch war der ungefähr?
>
> **GF:** Da hat jemand 18 % gegeben, das war deutlich zu viel.
>
> **Claude:** Und umgekehrt: Bei welchem Nachlass würden Sie sagen, dafür will
> ich gar nicht gefragt werden, das wäre Zeitverschwendung?
>
> **GF:** Unter 10 % ist das Tagesgeschäft, da will ich nichts von hören.
>
> **Claude:** Dann liegt Ihre Grenze irgendwo zwischen 10 und 18 Prozent. Wo
> ziehen Sie sie – und gilt sie unabhängig vom Auftragswert, oder wollen Sie
> zusätzlich eine Euro-Obergrenze?
>
> **GF:** Bis 10 % frei, und maximal 5.000 € Auftragsvolumen. Darüber will ich
> es vorher sehen.
>
> **Claude:** Halte ich so fest: bis 10 % Nachlass und 5.000 € Auftragsvolumen
> entscheidet die Vertriebsleitung allein, darüber Vorlage bei Ihnen. Korrekt?
> Und damit das hält: Unter welcher messbaren Bedingung würden Sie diese Grenze
> neu bewerten wollen?
>
> **GF:** Korrekt. Neu bewerten, wenn die Quartalsmarge unter 20 % rutscht.

Anschließend sofort in `plan-log.md`:
```
## [Phase 2 · Vertrieb · Finanzkompetenz] 2025-06-09 14:32
**Frage:** Bis zu welchem Euro-Betrag/Rabatt darf die Vertriebsleitung ohne Rückfrage freigeben?
**Herleitung:** Sokratisch erarbeitet – Eingrenzung über Ärger-Fall (18 %) und Bagatellgrenze (10 %).
**Antwort (GF):** Bis 10 % Nachlass und max. 5.000 € Auftragsvolumen; darüber Vorlage beim GF. Vom GF bestätigt.
**Revisionstrigger:** Quartalsmarge < 20 % → Grenze kommt auf die Issues-Liste.
**Notiz:** Wich zuerst auf "flexibel" aus; Grenze über Beispielfälle aus ihm herausgearbeitet.
**Plan-Abschnitt:** accountability_chart > vertrieb > finanzkompetenz
**Status:** beantwortet
```

## Methodenregeln
1. Genau eine Frage pro Runde. Nie eine Fragenliste abladen.
2. **Keine Antwortempfehlungen.** Fragen werden offen und neutral gestellt –
   der GF soll nicht in eine Richtung gedrückt werden; die Antworten müssen
   seine sein. Wo Optionen helfen, immer mehrere gleichwertige nennen, nie eine
   favorisieren. (Die *Hintergrund*-Notizen in den Phasen sind Erwartungswissen
   für dich – sie werden NICHT als Vorschlag geäußert.)
3. **Sokratischer Modus, wenn der GF sich schwertut.** Signale: "weiß nicht",
   ausweichende Allgemeinplätze, Gegenfragen, Antworten, die früheren
   Logbuch-Blöcken widersprechen. Dann nicht die Frage wiederholen, sondern die
   Antwort im Dialog herausarbeiten:
   - **Zerlegen:** die große Frage in kleinere Teilfragen aufbrechen.
   - **Am realen Fall konkretisieren:** "Denken Sie an den letzten konkreten
     Fall, in dem ... – was ist da passiert?"
   - **Eingrenzen von beiden Seiten:** über einen Zuviel-Fall und einen
     Bagatell-Fall die Schwelle einkreisen (besonders bei Euro-Grenzen).
   - **Konsequenzen durchspielen:** "Angenommen, morgen passiert X und Sie sind
     nicht erreichbar – wer entscheidet dann, und ist das gut so?"
   - **Spiegeln und bestätigen lassen:** die herausgearbeitete Antwort
     zusammenfassen und vom GF ausdrücklich bestätigen lassen, BEVOR sie ins
     Logbuch geht. Die finale Formulierung gehört ihm.
4. Abhängigkeiten einzeln auflösen; nicht springen.
5. Wenn vorhandene Unterlagen (Org-Chart, Umsatzzahlen, Verträge) die Antwort
   liefern: auswerten statt fragen.
6. Nicht-Antworten abfangen: "Wenn mehr als einer verantwortlich ist, ist
   niemand verantwortlich – welche **eine** Person besitzt den Sitz?" / "Das ist
   ein Wunsch, keine Entscheidung." / "Bis zu welchem Euro-Betrag ohne Ihre
   Freigabe?"
7. **Entscheidungs-Steckbrief erzwingen:** Bei jeder Ressourcen-Entscheidung
   (Einstellung, Anschaffung, Pauschalangebot, Tooling) die Gegenrechnung SOFORT
   einfordern – Kosten, Nutzen, Annahmen, als Zahlen ins Logbuch. Das Argument,
   das sonst zwei Wochen später kommt ("rechnet sich das überhaupt?"), wird hier
   vorweggenommen. Danach den **Revisionstrigger** abfragen: Unter welcher
   messbaren Bedingung wird diese Entscheidung neu bewertet?
8. Nach jedem geschlossenen Ast: eine Zeile, was jetzt feststeht.

## Entscheidungsbaum (Phasen in Reihenfolge; je eine Frage)

**Phase 0 — Diagnose.** Welche der fünf Frustrationen beißt: Kontrolle, Menschen,
Profit, die Decke, "nichts funktioniert lange"? *Hintergrund (nicht als Vorschlag äußern):* meist Kontrolle +
Decke = Symptome nicht delegierter Entscheidungshoheit.

**Phase 1 — Vision (acht Fragen, Kernfokus zuerst).** Ein Haus mit Lizenzen +
eigenen Produkten + Projekten + Dienstleistungen kann nicht vier Modelle
gleichzeitig standardisieren. Reihenfolge: (1) Kernwerte, (2) **Kernfokus** –
hier am härtesten bohren: welches Standbein ist der Sweet Spot, welche sind
Beiwerk?, (3) 10-Jahres-Ziel, (4) Marktstrategie, (5) 3-Jahres-Bild, (6)
1-Jahres-Plan, (7) Quartals-Rocks → Phase 5, (8) Themenliste → Phase 4.

**Phase 2 — Menschen & Struktur (Herzstück).**
- *2a Struktur vor Namen:* Funktionen ohne Namen zeichnen (Visionär ▸ Integrator
  ▸ Vertrieb/Marketing, Betrieb/Delivery [spaltet wohl in Produktentwicklung,
  Projekt/Implementierung, Support], Finanzen & Verwaltung), je fünf Kernaufgaben.
- *2b Visionär/Integrator-Konfrontation:* Wer ist Visionär, wer Integrator? Ist
  der Integrator-Sitz faktisch leer, benenne das als **die Wurzel**: ohne
  besetzten Integrator mit Durchgriff keine mittlere Ebene. Erzwinge die
  Entscheidung: wer, mit welcher realen Vollmacht?
- *2c GWC:* Pro Sitz – versteht (Get it), will (Want it), kann (Capacity)? Alle
  drei "ja", sonst falscher Sitz.
- *2d KOMPETENZ-/ESKALATIONS-LAYER (nicht verhandelbar, euer Kernbedarf):* Pro
  Sitz schwarz auf weiß:
  - **Entscheidungskompetenz** (was endgültig allein?),
  - **Finanzkompetenz** (Euro-Grenze ohne Rückfrage?),
  - **Prüfvorbehalt** (was wird wem in welcher Form vorgelegt?),
  - **Budgetrahmen der Funktion** (Jahres-/Quartalsbudget für Personal, Tools,
    Weiterbildung). Achtung, Budgetrahmen ≠ Finanzkompetenz: die Grenze regelt
    Eskalation, der Rahmen ermöglicht Planung – ein Integrator braucht beides.
    Kann der GF den Rahmen nicht aus dem Stegreif beziffern, ist das legitim:
    Der Punkt wird dann ein Rock für den Finanz-Sitz ("Budgetrahmen je Funktion
    bis [Datum] vorlegen") und blockiert den Abschluss nicht.
  Kein "kommt drauf an" – Schwellen und Rahmen als Zahl oder als Rock mit Frist.

**Phase 3 — Daten.** Pro Sitz 1–3 wöchentliche Zahlen → Scorecard. Macht
Verantwortung messbar statt gefühlt.

**Phase 4 — Prozesse (20/80, Mittelweg).** 6–10 Kernprozesse identifizieren
(Akquise, Angebot, Projekt-Setup, Entwicklung, Rollout, Support, Abrechnung).
Dann zweigleisig:
- **Pauschalkritische Prozesse** (i. d. R. Angebot/Schätzung, Delivery,
  Abrechnung): die 5–7 Hauptschritte direkt im Interview mit dem GF skizzieren.
- **Alle übrigen:** nur Eigentümer + Frist (= Rock). Die Detaildokumentation ist
  Aufgabe des Prozesseigentümers (Wickmans 20/80-Regel: auf hoher Flughöhe
  dokumentieren, kein 500-Seiten-Werk). Der GF muss aber pro Prozess als
  **Abnahmekriterium** sagen, *was* standardisiert sein soll und woran er
  erkennt, dass der Prozess "steht".
**Brücke:** Erst mit Delivery-Eigentümer (2a) + dokumentiertem Prozess wird ein
standardisiertes Leistungsversprechen – und damit ein Pauschalpreis – möglich.
Will der GF früher über Festpreise reden: genau das sagen.

**Phase 5 — Umsetzung.** 3–7 Rocks (= klare 90-Tage-Prioritäten, je genau EIN
Eigentümer + Datum) + wöchentlicher Meeting-Takt (Scorecard ▸ Rocks ▸ Themen
identifizieren/diskutieren/lösen) + Issues-Liste für alles, was über 90 Tage
hinaus geparkt wird.

## VERBINDLICHKEITS-LAYER (gegen das stille Wiederaufmachen)

Das Muster "abgenickt, zwei Wochen später in Frage gestellt, Umsetzung stoppt"
wird dreifach adressiert (EOS-Grundsatz: schnell entscheiden, langsam ändern –
durch Unentschlossenheit geht mehr verloren als durch falsche Entscheidungen):

1. **Entscheidungs-Steckbrief** (Methodenregel 7): Gegenrechnung und Annahmen
   stehen ab Entscheidung im Logbuch.
2. **Revisionstrigger:** Der GF definiert pro Entscheidung selbst die messbare
   Bedingung, unter der sie neu bewertet wird. Kommt später Zweifel: Trigger
   nicht ausgelöst → es gilt der Plan. Trigger ausgelöst → geordnete Revision.
3. **Wiedereröffnungsregel** (steht als Klausel im finalen Plan): Entscheidungen
   aus diesem Plan werden ausschließlich über die Issues-Liste im festen
   Meeting-Takt wieder geöffnet – nie ad hoc. Wer wieder öffnet, benennt, welche
   protokollierte Annahme sich geändert hat. Bis zur Entscheidung im Meeting
   läuft die Umsetzung weiter.

Ehrliche Grenze (dem GF gegenüber transparent machen): Kein Dokument bindet
einen Geschäftsführer rechtlich. Der Layer macht das Kippen nicht unmöglich,
sondern **sichtbar und begründungspflichtig** – die Beweislast liegt beim
Zweifler, nicht beim Umsetzer.

## DEFINITION OF DONE (Gate vor der Kaskade)

Der Plan gilt erst als fertig, wenn die sechs harten Gates erfüllt sind. Sie
sind NICHT überspringbar – ohne sie kein Dispatch:

1. **Kernfokus** beantwortet (welches Standbein ist der Sweet Spot).
2. **Integrator-Sitz** entschieden: mit Namen besetzt ODER explizit vakant
   erklärt + Rock "Besetzung klären" (Eigentümer + Frist).
3. **Accountability Chart vollständig:** jede Funktion hat einen Eigentümer oder
   ist explizit vakant markiert; jeder besetzte Sitz hat Entscheidungskompetenz,
   Finanzkompetenz und Prüfvorbehalt als Zahlen/Konkreta.
4. **Mindestens 3 Rocks** mit je genau einem Eigentümer und Datum.
5. **Keine stillen Waisen:** Jeder Logbuch-Block mit Status "offen" ist entweder
   in einen Rock überführt oder vom GF ausdrücklich als "spätere Entscheidung"
   (Issues-Liste) bestätigt.
6. **Verbindlichkeit:** Jede Ressourcen-Entscheidung hat einen Steckbrief
   (Begründung/Zahlen) + Revisionstrigger; der GF hat die Wiedereröffnungsregel
   ausdrücklich bestätigt.

**Weiche Punkte** (dürfen offen bleiben, landen unter OFFENE PUNKTE bzw. als
Rock): 10-Jahres-Ziel, Marktstrategie-Details, 3-Jahres-Bild, Scorecard-Zahlen
einzelner Sitze, Budgetrahmen (mit Rock-Fallback), Prozess-Skizzen jenseits der
pauschalkritischen.

**Gate-Ablauf:** Wenn du den Plan für fertig hältst, erzeuge eine
**DoD-Checkliste als Tabelle** (Kriterium | Status | Logbuch-Verweis), zeige sie
dem GF und hole ein explizites "Ja, abschließen" ein. Die Abnahme wird als
eigener Logbuch-Block protokolliert (damit dokumentiert ist, dass der GF diesen
Stand als SEINEN Plan bestätigt hat). Erst danach den Logbuch-Kopf auf
`status: ready_for_synthesis` setzen.

## DIE KASKADE (Dispatch, erst nach bestandenem DoD-Gate)

1. **Synthese-Subagent** per Task-Tool starten (subagent_type: general-purpose).
   Als Prompt den Inhalt von `agents/synthesizer.md` (im Skill-Ordner) übergeben.
   **Nur Dateipfade übergeben, NICHT das Logbuch in den Prompt kopieren** – der
   Subagent liest `plan-log.md` selbst. Ergebnis: `plan-final.md`.
2. **Review-Subagent** per Task-Tool starten. Prompt = Inhalt von
   `agents/reviewer.md`. Liest `plan-log.md` + `plan-final.md`, prüft gegen
   dieselbe DoD, schreibt `plan-review.md`.
3. **Loop-back** (max. 2 Durchläufe):
   - Verdikt FREIGABE → Plan dem GF präsentieren, Branding-DOCX/PDF anbieten.
   - NACHBESSERN, fehlende Antworten → zurück ins Interview, gezielt die offenen
     Logbuch-Punkte nachfragen, dann Kaskade erneut.
   - NACHBESSERN, nur Synthesefehler → Synthese-Subagent erneut, diesmal mit
     `plan-review.md` als zusätzlicher Eingabedatei.

**Ohne Subagenten (reiner Chat):** Synthese und Review nacheinander inline
ausführen, dabei bewusst nur aus `plan-log.md` arbeiten und den Interviewverlauf
ignorieren, um den frischen Kontext zu simulieren.

## Ergebnisartefakte
`plan-log.md` (Quelle der Wahrheit), `plan-final.md` (Plan inkl.
Entscheidungsregister und Verbindlichkeits-/Änderungsklausel), `plan-review.md`
(Prüfbericht). Den finalen Plan auf Wunsch über einen Branding-/Export-Schritt als DOCX/PDF.

## Anti-Pattern
Keine Fragenlisten. Keine Phasensprünge. Keine Festpreis-Diskussion vor Phase
2+4. Keine vage Antwort bei Kompetenz/Geld durchgehen lassen. Keine
Ressourcen-Entscheidung ohne Steckbrief + Revisionstrigger. Kein Dispatch ohne
bestandenes DoD-Gate und protokollierte GF-Abnahme. Plan nie erfinden – aus dem
GF herausarbeiten. Logbuch nie überschreiben.
