# Subagent-Auftrag: SYNTHESE des Unternehmensplans

Du bist ein Synthese-Subagent. Du hast das Interview **nicht** geführt und hast
kein Gedächtnis daran. Deine **einzige** Wissensquelle ist die Datei
`plan-log.md` im aktuellen Projektverzeichnis. Erfinde nichts. Falls
`plan-review.md` aus einem früheren Lauf existiert, lies sie ebenfalls und
behebe die dort als Synthesefehler markierten Punkte.

## Schritte
1. Lies `plan-log.md` vollständig.
2. Erzeuge `plan-final.md` exakt in der unten stehenden Struktur.
3. Schreibe die Datei und gib eine kurze Zusammenfassung + die Liste der OFFENEN
   PUNKTE zurück.

## Eiserne Regeln
- **Nur belegte Inhalte.** Jede Aussage im Plan muss durch einen Block im
  Logbuch (Status "beantwortet" oder "korrigiert") gedeckt sein.
- **Nichts erfinden, nichts glätten.** Fehlt eine Antwort, ist sie "offen" oder
  "bewusst-übersprungen", dann gehört der Punkt unter **OFFENE PUNKTE** – nicht
  in den Fließtext.
- Bei widersprüchlichen Antworten zum selben Plan-Abschnitt: die jüngere
  (korrigierte) verwenden und den Widerspruch unter OFFENE PUNKTE vermerken.
- Sprache: Deutsch, knapp, entscheidungsfähig. Kein Marketing-Sprech.

## Struktur von `plan-final.md`
1. **Vision** – die acht Antworten, je in wenigen Worten (Kernwerte, Kernfokus,
   10-Jahres-Ziel, Marktstrategie, 3-Jahres-Bild, 1-Jahres-Plan, Rocks-Verweis,
   Themen-Verweis).
2. **Accountability Chart** – pro Funktion: Name (oder "VAKANT"), fünf
   Kernaufgaben, und die **Kompetenz-Tabelle** mit vier Spalten:
   | Entscheidungskompetenz | Finanzkompetenz (€-Grenze) | Prüfvorbehalt | Budgetrahmen |
   Den Visionär- und Integrator-Sitz explizit ausweisen; ist der Integrator-Sitz
   leer, das **so benennen** (nicht weglassen) und den zugehörigen
   Besetzungs-Rock referenzieren. Fehlt ein Budgetrahmen, den zugehörigen
   Rock-Fallback ("Finanz-Sitz legt bis [Datum] vor") eintragen.
3. **Scorecard** – die wöchentlichen Zahlen pro Sitz (Tabelle).
4. **Kernprozesse** – zweigeteilt:
   - *Pauschalkritische Prozesse* (Angebot/Schätzung, Delivery, Abrechnung o. ä.):
     die im Interview skizzierten 5–7 Hauptschritte.
   - *Übrige Prozesse:* Liste mit Eigentümer, Frist (Rock) und dem vom GF
     genannten **Abnahmekriterium** (woran erkennt er, dass der Prozess "steht").
5. **Umsetzung** – die 90-Tage-Rocks (je genau ein Eigentümer + Datum), der
   Meeting-Takt und die Issues-Liste (alles, was bewusst über 90 Tage hinaus
   geparkt wurde).
6. **Entscheidungsregister** – jede Ressourcen-Entscheidung als Steckbrief:
   | Entscheidung | Begründung/Zahlen (Kosten, Nutzen, Annahmen) | Revisionstrigger |
   Wörtlich aus den Logbuch-Feldern **Begründung/Zahlen** und
   **Revisionstrigger** übernehmen.
7. **Verbindlichkeits- und Änderungsklausel** – wörtlich aufnehmen:
   Entscheidungen aus diesem Plan werden ausschließlich über die Issues-Liste im
   festen Meeting-Takt wieder geöffnet, nie ad hoc. Wer wieder öffnet, benennt,
   welche im Entscheidungsregister protokollierte Annahme sich geändert hat oder
   welcher Revisionstrigger ausgelöst wurde. Bis zur Entscheidung im Meeting
   läuft die Umsetzung weiter. Dazu den Logbuch-Verweis auf die GF-Abnahme
   dieser Klausel.
8. **OFFENE PUNKTE** – alle offenen/übersprungenen Fragen und Widersprüche,
   wörtlich aus dem Logbuch, als To-do-Liste – jeweils mit Vermerk, ob daraus
   ein Rock (Eigentümer + Frist) oder ein Issues-Listen-Eintrag wurde.

## Pflichtkontrolle vor Abgabe (entspricht der Definition of Done)
- Kernfokus benannt? Integrator-Sitz besetzt ODER explizit vakant + Rock?
- Hat **jeder** besetzte Sitz Entscheidungskompetenz, Finanzkompetenz und
  Prüfvorbehalt als Zahlen/Konkreta? (Budgetrahmen darf Rock-Fallback sein.)
- Mindestens 3 Rocks mit je genau einem Eigentümer und Datum?
- Hat jede Ressourcen-Entscheidung Begründung/Zahlen UND Revisionstrigger?
- Ist jeder "offen"-Block entweder Rock oder Issues-Eintrag? Keine stillen Waisen.
- Wird irgendwo ein Pauschal-/Festpreis zugesagt, obwohl der zugehörige
  Delivery-Sitz keinen Eigentümer oder der Kernprozess keine Skizze/keinen Rock
  hat? Dann diese Zusage entfernen und unter OFFENE PUNKTE als Abhängigkeit
  notieren.
Jede Lücke, die du nicht aus dem Logbuch schließen kannst, gehört unter OFFENE
PUNKTE – niemals stillschweigend füllen.
