# Quellen und Rechenlogik

Jede Zahl, die die App berechnet, steht hier mit ihrer Herkunft. Wo eine Methode
umstritten ist, steht die Kritik dabei.

---

## 1. Nährwertdaten

**Open Food Facts** — `https://world.openfoodfacts.org/api/v2/product/<EAN>.json`
Freie Produktdatenbank, ODbL-Lizenz, kein API-Key, keine Registrierung.
Die App fragt gezielt nur die benötigten Felder ab (`fields=`-Parameter), um Datenvolumen
und Serverlast klein zu halten.

*Einschränkung:* Die Daten sind community-gepflegt. Tippfehler und veraltete Rezepturen kommen
vor. Die App prüft deshalb jeden Treffer gegen die Atwater-Faktoren (4 kcal/g Protein,
4 kcal/g Kohlenhydrate, 9 kcal/g Fett) und warnt bei über 15 % Abweichung zwischen deklarierten
und errechneten Kalorien.

**Für Grundnahrungsmittel besser geeignet:**
- USDA FoodData Central — `https://fdc.nal.usda.gov/api-guide.html` (gratis, API-Key per Mail)
- Bundeslebensmittelschlüssel (BLS), Max Rubner-Institut — deutscher Referenzstandard,
  kostenpflichtig lizenziert
- Souci-Fachmann-Kraut — Standardwerk der Lebensmittelanalytik, kostenpflichtig

---

## 2. Energiebedarf

**Grundumsatz — Mifflin-St Jeor (1990)**
Mifflin MD, St Jeor ST, et al. *A new predictive equation for resting energy expenditure in
healthy individuals.* Am J Clin Nutr 51(2):241–247.

    Männer:  10 × kg + 6,25 × cm − 5 × Jahre + 5
    Frauen:  10 × kg + 6,25 × cm − 5 × Jahre − 161

Gilt gegenüber Harris-Benedict als genauer für Nicht-Adipöse. Bei sehr hohem Muskelanteil
unterschätzt jede körpergewichtsbasierte Formel den Bedarf — dann ist die
Katch-McArdle-Formel (über fettfreie Masse) die bessere Wahl.

**Gesamtumsatz** = Grundumsatz × PAL + Trainingsanteil
Der PAL-Faktor (Physical Activity Level) bildet den Alltag ohne Training ab (D-A-CH-Referenzwerte
der DGE). Trainingsenergie wird pro Einheit über MET × kg × Stunden geschätzt
(Ainsworth et al., *Compendium of Physical Activities*, 2011) und zur Hälfte addiert,
weil ein PAL von 1,5–1,6 bereits einen Teil sportlicher Aktivität enthält. Doppelt gerechnete
Trainingskalorien sind der häufigste Fehler in Tracking-Apps.

Angesetzte MET-Werte: Handball 7,0 · Krafttraining 5,0 · Sonstiges 6,5.

---

## 3. Makronährstoffe

**Protein — 1,4 bis 2,0 g/kg**
Jäger R, Kerksick CM, Campbell BI, et al. (2017). *International Society of Sports Nutrition
Position Stand: Protein and exercise.* J Int Soc Sports Nutr 14:20.
Voreinstellung der App: 1,8 g/kg.

**Kohlenhydrate — 5 bis 7 g/kg an Belastungstagen**
Thomas DT, Erdman KA, Burke LM (2016). *Position of the Academy of Nutrition and Dietetics,
Dietitians of Canada, and the American College of Sports Medicine: Nutrition and Athletic
Performance.* Med Sci Sports Exerc 48(3):543–568.
Die App senkt das Kohlenhydratziel an Tagen ohne Einheit um 2 g/kg (Carbohydrate Periodisation),
Untergrenze 3 g/kg.

**Fett** — Restenergie nach Protein und Kohlenhydraten, Untergrenze 35 g/Tag.

**Mikronährstoffe** — D-A-CH-Referenzwerte der Deutschen Gesellschaft für Ernährung.
Die App trackt sie nicht; für Sportler mit reduziertem Fleischanteil sind vor allem Eisen,
Zink, B12 und Jod relevant.

---

## 4. Trainingslast

**session-RPE (sRPE)**
Foster C (1998). *Monitoring training in athletes with reference to overtraining syndrome.*
Med Sci Sports Exerc 30(7):1164–1168.
Foster C, Florhaug JA, Franklin J, et al. (2001). *A new approach to monitoring exercise
training.* J Strength Cond Res 15(1):109–115.

    Last einer Einheit = RPE (Skala 1–10) × Dauer in Minuten  [Arbitrary Units, AU]

Der entscheidende Vorteil: Ein 90-Minuten-Handballtraining und ein 60-Minuten-Krafttraining
werden auf einer gemeinsamen Skala vergleichbar. RPE wird etwa 30 Minuten nach Ende erhoben —
früher überlagert die letzte harte Übung das Gesamturteil.

**Monotonie und Strain** (Foster 1998)

    Monotonie = Mittelwert der Tageslasten / Standardabweichung der Tageslasten
    Strain     = Wochenlast × Monotonie

Foster fand einen Zusammenhang zwischen hoher Monotonie (> 2,0) und Infekten sowie Stagnation.
Praktische Folge: Ein echter Ruhetag senkt die Monotonie stärker als ein durchgehend lockeres
Programm.

**Interne vs. externe Last**
Impellizzeri FM, Marcora SM, Coutts AJ (2019). *Internal and External Training Load: 15 Years
On.* Int J Sports Physiol Perform 14(2):270–273.

**Acute:Chronic Workload Ratio — bewusst ohne Ampel**
Gabbett TJ (2016). *The training-injury prevention paradox.* Br J Sports Med 50(5):273–280.
Diese Arbeit hat die ACWR populär gemacht. Die Methodik ist inzwischen umfassend kritisiert:
- Impellizzeri FM, Woodcock S, Coutts AJ, et al. (2020). *Acute to Random Workload Ratio is
  'as' associated with injury as Acute to Actual Chronic Workload Ratio.* / *Conceptual issues
  and fundamental pitfalls.* Int J Sports Physiol Perform.
- Lolli L, Batterham AM, Hawkins R, et al. (2019). *Mathematical coupling causes spurious
  correlation within the conventional acute-to-chronic workload ratio calculations.*
  Br J Sports Med 53(15):921–922.

Die App zeigt das 7:28-Verhältnis deshalb nur als Beschreibung deiner Belastungsverteilung,
ohne Farbcodierung und ohne Verletzungsprognose — und erst ab drei Wochen Datenhistorie.

---

## 5. Erholung und Befinden

**Hooper-Index**
Hooper SL, Mackinnon LT (1995). *Monitoring overtraining in athletes: recommendations.*
Sports Med 20(5):321–327.
Vier Items — Schlafqualität, Müdigkeit, Stress, Muskelkater — je 1 bis 7. Summe 4 bis 28,
niedrig ist besser.

**Warum subjektiv vor objektiv**
Saw AE, Main LC, Gastin PB (2016). *Monitoring the athlete training response: subjective
self-reported measures trump commonly used objective measures.* Br J Sports Med 50(5):281–291.
Kernbefund: Selbstauskunft reagiert sensibler und konsistenter auf Belastungsänderungen als
objektive Marker. Ein 20-Sekunden-Fragebogen schlägt ein Armband.

**Referenz statt Absolutwert**
Die App vergleicht deinen Tageswert mit deinem eigenen 14-Tage-Schnitt (z-Standardisierung),
sobald mindestens vier Tage erfasst sind. Ein Hooper-Wert von 12 sagt für sich genommen nichts —
12 bei einem Schnitt von 9 ist ein Signal, 12 bei einem Schnitt von 15 ist Erholung.

**Konsens zur Regeneration**
Kellmann M, Bertollo M, Bosquet L, et al. (2018). *Recovery and Performance in Sport: Consensus
Statement.* Int J Sports Physiol Perform 13(2):240–245.

**Herzratenvariabilität**
Plews DJ, Laursen PB, Stanley J, et al. (2013). *Training adaptation and heart rate variability
in elite endurance athletes: opening the door to effective monitoring.* Sports Med 43(9):773–781.
Buchheit M (2014). *Monitoring training status with HR measures: do all roads lead to Rome?*
Front Physiol 5:73.
Entscheidend: der **Wochenmittelwert** des rMSSD, nie der Einzeltag. Immer unter gleichen
Bedingungen messen — morgens, direkt nach dem Aufwachen, vor dem Aufstehen.

**Schlaf**
Fullagar HHK, Skorski S, Duffield R, et al. (2015). *Sleep and athletic performance.*
Sports Med 45(2):161–186.

---

## 6. Krafttraining

**Geschätztes 1RM — Epley (1985)**

    e1RM = Gewicht × (1 + Wiederholungen / 30)

RIR (Reps in Reserve) wird als zusätzliche Wiederholung eingerechnet. Ab etwa zehn
Wiederholungen wird jede 1RM-Schätzformel deutlich ungenau.

**RIR-basierte RPE**
Zourdos MC, Klemp A, Dolan C, et al. (2016). *Novel resistance training-specific rating of
perceived exertion scale measuring repetitions in reserve.* J Strength Cond Res 30(1):267–275.

**Volumen**
Schoenfeld BJ, Ogborn D, Krieger JW (2017). *Dose-response relationship between weekly
resistance training volume and increases in muscle mass.* J Sports Sci 35(11):1073–1082.
Die App summiert das Tonnage-Volumen (Last × Wiederholungen) je Übung über sieben Tage.

---

## 7. Handballspezifisches Anforderungsprofil

- Karcher C, Buchheit M (2014). *On-court demands of elite handball, with special reference to
  playing positions.* Sports Med 44(6):797–814. — Positionsspezifische Belastung; für
  Rückraumspieler besonders relevant.
- Michalsik LB, Aagaard P, Madsen K (2013/2015). *Locomotion characteristics and match-induced
  impairments in physical performance in male elite team handball players.* Int J Sports Med.
- Wagner H, Finkenzeller T, Würth S, von Duvillard SP (2014). *Individual and team performance
  in team-handball: a review.* J Sports Sci Med 13(4):808–816.

---

## Grenzen

Alle Zielwerte der App sind Schätzungen aus Populationsformeln, keine Messwerte. Der reale
Grundumsatz kann um ±10 % abweichen; nur eine indirekte Kalorimetrie misst ihn tatsächlich.
Die App ersetzt keine sportmedizinische oder ernährungstherapeutische Beratung.

Der belastbarste Wert in dieser App ist nicht die Kalorienzahl, sondern die Kombination aus
sRPE-Verlauf und täglichem Befinden über mehrere Wochen. Deren Aussagekraft entsteht erst
durch Konsistenz.

---

## 8. ADHS-Schicht

Alles hier ist Verhaltensgerüst, keine Behandlung. Maik ist psychiatrisch angebunden; die App
gibt keine Medikationsempfehlungen.

**Essen an Zeitanker statt an Hunger**
Stimulanzien der Amfetamin-Gruppe senken den Appetit über die Wirkdauer — verminderter Appetit
und Gewichtsverlust sind in den Fachinformationen zu Lisdexamfetamin als sehr häufige
Nebenwirkungen geführt. Wer auf das Hungersignal wartet, isst während der Wirkung zu wenig und
nach dem Nachlassen zu viel. Die App leitet vier Essensfenster aus einer einzigen Größe ab, der
Einnahmezeit, und legt sie auf −20 min, +4 h, +7 h und +10 h. Grundlage ist der typische
Wirkverlauf: Wirkeintritt nach etwa einer Stunde, Spitze nach dreieinhalb bis viereinhalb
Stunden, Nachlassen nach zehn bis zwölf Stunden.
Proteinverteilung bewusst vorn: 30 / 30 / 15 / 25 Prozent des Tagesziels.

**Wenn-dann-Regeln (Implementation Intentions)**
Gollwitzer PM (1999). *Implementation intentions: Strong effects of simple plans.*
American Psychologist 54(7):493–503.
Gollwitzer PM, Sheeran P (2006). *Implementation intentions and goal achievement: a
meta-analysis of effects and processes.* Advances in Experimental Social Psychology 38:69–119.
Gawrilow C, Gollwitzer PM (2008). *Implementation intentions facilitate response inhibition in
children with ADHD.* Cognitive Therapy and Research 32:261–280.
Gawrilow C, Gollwitzer PM, Oettingen G (2011). *If-then plans benefit executive functions in
children with ADHD.* Journal of Social and Clinical Psychology 30(6):616–646.
Der Wirkmechanismus ist Delegation: Die Situation löst die Handlung aus, statt dass im Moment
entschieden werden muss. Genau die Entscheidung im Moment ist bei ADHS der teure Schritt.

**Kein Streak, sondern Reparatur**
Erhöhtes Delay Discounting bei ADHS — der Wert einer Belohnung fällt mit der Verzögerung
steiler ab als bei Kontrollgruppen. Praktische Folge: Rückmeldung muss sofort kommen, nicht am
Wochenende. Streaks wirken deshalb in die falsche Richtung — sie setzen die gesamte Belohnung
auf einen fernen Zeitpunkt und entwerten mit einem Aussetzer alles Bisherige.
Die App zählt stattdessen erfasste Tage der letzten 14 und begrüßt die Rückkehr nach einer
Lücke ausdrücklich. Gewohnheitsbildung braucht ohnehin länger und verträgt Aussetzer:
Lally P, van Jaarsveld CHM, Potts HWW, Wardle J (2010). *How are habits formed: Modelling habit
formation in the real world.* European Journal of Social Psychology 40(6):998–1009 —
Median 66 Tage, und einzelne ausgelassene Gelegenheiten beeinträchtigten den Aufbau nicht
messbar.

**Drei Hauptaufgaben und der kleinste erste Schritt**
Barkley RA (1997). *Behavioral inhibition, sustained attention, and executive functions:
constructing a unifying theory of ADHD.* Psychological Bulletin 121(1):65–94.
Kernproblem ist nicht Wissen, sondern Handlungsinitiierung und Arbeitsgedächtnis. Daraus folgen
zwei Konsequenzen für die Oberfläche: die Zahl offener Entscheidungen klein halten, und für
jede Aufgabe eine erste Handlung hinterlegen, die unter einer Minute dauert.

**Nachmittagstief**
Kein Literaturwert, sondern Maiks eigene Beobachtung (15:00–17:00). Die App warnt, wenn eine
Hauptaufgabe dorthin gelegt wird.

**Bewegung als Hebel**
Mehren A, Reichert M, Coghill D, et al. (2020). *Physical exercise in attention deficit
hyperactivity disorder — evidence and implications for the treatment of borderline personality
disorder.* Borderline Personality Disorder and Emotion Dysregulation 7:1.
Cerrillo-Urbina AJ, García-Hermoso A, Sánchez-López M, et al. (2015). *The effects of physical
exercise in children with ADHD: a systematic review and meta-analysis of randomized control
trials.* Child: Care, Health and Development 41(6):779–788.
Akute aerobe Belastung verbessert Aufmerksamkeit und exekutive Funktionen kurzfristig. Für Maik
heißt das: Training ist nicht nur Belastung, sondern auch ein Fokusfenster danach.

**Fokusfenster nach dem Training**
Mehren A, Özyurt J, Lam AP, et al. (2019). *Acute Effects of Aerobic Exercise on Executive
Function and Attention in Adult Patients With ADHD.* Frontiers in Psychiatry 10:132.
DOI 10.3389/fpsyt.2019.00132 (über PubMed recherchiert, PMID 30971959).
30 Minuten moderates Radfahren verbesserten bei 23 Erwachsenen mit ADHS die Reaktionszeiten im
Flanker-Test — bei 23 gesunden Kontrollpersonen nicht.
*Grenze:* Einzelstudie, kleine Stichprobe, anderes Belastungsprotokoll als Handball oder
Krafttraining. Die **Dauer** eines solchen Fensters ist nicht belegt. Die App schlägt es
deshalb nur vor und überlässt die Bewertung der eigenen Erfahrung.

**Morgenlicht und innere Uhr**
Snitselaar MA, Smits MG, van der Heijden KB, Spijker J. *Sleep and Circadian Rhythmicity in
Adult ADHD and the Effect of Stimulants.* Journal of Attention Disorders.
DOI 10.1177/1087054713479663 (PMID 23509113).
Erwachsene mit ADHS zeigen längere objektive Einschlaflatenz, spätere Aufwachzeit, verzögerten
Melatoninanstieg — das Bild einer verzögerten Schlafphase. Stimulanzien verschieben die
Rhythmik zusätzlich nach hinten, Lichttherapie in Richtung Morgentyp.

Fargason RE, Fobian AD, Hablitz LM, et al. (2017). *Correcting delayed circadian phase with
bright light therapy predicts improvement in ADHD symptoms: A pilot study.* Journal of
Psychiatric Research 91:105–110. DOI 10.1016/j.jpsychires.2017.03.004 (PMID 28327443).
Zwei Wochen morgens 30 Minuten 10.000 Lux verschoben den Melatoninanstieg um 31 Minuten und die
Schlafmitte um 57 Minuten nach vorn; die Verschiebung korrelierte mit niedrigeren
ADHS-Symptomwerten.
*Grenze:* Pilotstudie mit wenigen Teilnehmern, Therapielicht mit 10.000 Lux. Tageslicht am
Fenster ist deutlich schwächer. Der Schritt „ans Fenster" in der Morgenroutine ist deshalb
plausibel begründet, aber nicht in dieser Stärke belegt.

**Startritual — zwei Minuten**
Kein eigener Studienbeleg. Die Begründung ist die Handlungsinitiierung als Kernproblem
(Barkley 1997) plus das Prinzip des kleinsten Starts. Als solches in der App gekennzeichnet:
Die Zwei-Minuten-Grenze ist eine Konvention, keine Wirkgröße.

Recherchiert über PubMed.

---

## 9. Lebensbereiche (ab V5)

Die folgenden Module stammen aus Masterplan V8 und dem Evidenzdossier V1. Bewertet wird nach
vier Stufen — A stark, B mittel, C begrenzt, D Erfahrungswert. Die Stufe steht in der App an
der jeweiligen Aussage, nicht nur hier.

### 9.1 Haushalt — Stufe C

Kein einziges Modul dieser Seite beruht auf einer kontrollierten Studie zum Sauberhalten von
Küche, Zimmer und Auto bei Erwachsenen mit ADHS. Es gibt sie nicht. Gestützt sind nur die
allgemeineren Bausteine:

- Ergotherapeutischer Fachkonsens zu Umgebungsanpassung, Routine und Aufgabenanpassung bei
  Erwachsenen mit ADHS. *Grenze:* das Papier benennt selbst ausdrücklichen Forschungsbedarf.
- Scoping Review zu Alltagsroutinen und Gewohnheiten bei ADHS, 31 Studien. *Grenze:* nur sechs
  davon sind Interventionen, und die Erwachsenenlage ist dünn.
- W3C/WCAG „Help Users Focus": kurze kritische Pfade, wenig Ablenkung, klare Orientierung.
  *Grenze:* Zugänglichkeitsstandard, keine klinische Wirksamkeitsstudie.

**Konsequenz im Code:** Genau ein sichtbarer nächster Schritt, drei Reaktionen, kein
Rückstandsspeicher über Nacht, und ein Evidenzhinweis C am Fuß der Seite. Die
Reinigungsfrequenzen (zweimal wöchentlich kurz saugen, wöchentlich vollständig, feuchtes
Staubwischen) sind persönliche Startwerte bei zwei Hunden und einer Katze — **keine
medizinischen Grenzwerte**, und für Allergie oder Asthma ausdrücklich nicht gültig.

**Sicherheitsregeln, die nicht verhandelbar sind:** kein Nasswischen eines unbekannten
Holz- oder Laminatbodens; keine Flüssigkeit direkt auf Elektronik; keine rutschigen
Pflegemittel an Lenkrad, Schalthebel oder Pedalen; nach Kontakt mit rohen tierischen
Lebensmitteln getrennte Reinigung von Händen, Geräten und Flächen. Das ist der einzige
Küchenschritt, der wirklich sicherheitsrelevant ist — der Rest ist Ordnung, kein Risiko.

### 9.2 Body Doubling und Fokusmodus — Stufe C

Eagle et al. (2024): Befragungs- und Designstudie mit 220 neurodivergenten Teilnehmenden.
Beschreibt reale, virtuelle und aufgezeichnete Formen sowie Einsatzfelder wie Lernen, Putzen
und Bewegung.
*Grenze:* **kein Wirksamkeits-RCT.** Was berichtet wird, sind wahrgenommene Vorteile. Deshalb
steht Body Doubling in der App als persönliche Fokusstrategie, nie als ADHS-Behandlung.

Community-Berichte nennen übereinstimmend die Videosuche als eigene Ablenkung. Der Fokusmodus
startet deshalb ohne Auswahl, ohne Video und ohne Feed.

Der Ablenkungsparkplatz folgt der JITAI-Designlogik (richtige Hilfe, richtige Menge, richtiger
Zeitpunkt) — ein Designrahmen, kein Wirksamkeitsbeleg für die einzelne Funktion.

### 9.3 Ergebnis vorstellen statt Weg planen — Stufe B

Randomisierte Studie mit 196 Erwachsenen, davon 98 mit ADHS: episodisches Zukunftsdenken half
beim prospektiven Gedächtnis, und zwar besonders die **ergebnisorientierte** Vorstellung. Die
prozessorientierte Variante half der ADHS-Gruppe nur moderat.
*Grenze:* erste Studie, Replikation steht aus. In der App als fünf Sekunden im
Werkzeugkasten umgesetzt, nicht als Pflichtschritt.

**Gegenbefund, der mitgehört:** In einer ADHS-Internetintervention verbesserten einfache
Standard-SMS weder Modulerfüllung noch Logins noch Strategieanwendung. Mehr Erinnerungen sind
nicht besser. Relevanz, Handlungsschritt, Kontext und Bestätigung schlagen Häufigkeit.

### 9.4 Medikamentenmodul — Stufe A für das Monitoring, keine Stufe für Entscheidungen

- NICE NG87 (ADHS): gemeinsame Entscheidung, Umweltanpassung, Behandlung und Monitoring von
  Wirkung, Nebenwirkungen, Gewicht, Schlaf, Puls und Blutdruck.
- NICE NG222 (Depression): frühe Überprüfung, Nebenwirkungen, Adhärenz, Absetzsymptome.
- Fachinformation Lisdexamfetamin: laufendes Gewicht-, Herz-Kreislauf- und psychiatrisches
  Monitoring; **erhöhtes Risiko für ein Serotoninsyndrom bei Kombination mit serotonergen
  Arzneimitteln.**
- Fachinformation Escitalopram: abruptes Absetzen vermeiden, mögliche Absetzsymptome.

**Konsequenz im Code:** Die App zeigt die Serotonin-Information genau einmal, sachlich, ohne
die verordnete Kombination zu bewerten und ohne zum Absetzen aufzufordern. Sie nennt die
Warnzeichen, die nicht auf den Wochenbericht warten. Nach einer vergessenen Einnahme sagt sie
bewusst **nichts** — kein Vorschlag, keine Ersatzdosis. Sie erzeugt keinen verkürzten
klinischen Score und leitet keine Dosis- oder Wechselentscheidung ab.

Zwei Ebenen statt täglicher Befragung: wöchentlich 1–2 Minuten, alle zwei Wochen 3–5 Minuten.
Begründung aus einer systematischen Übersicht zu Stimmungsmonitoring: Monitoring kann nützen,
erzeugt aber auch Belastung. *Grenze dieser Quelle:* untersucht wurde bipolare Störung.

Zur Adhärenz: Meta-Analyse über 9 RCTs mit 1.159 Teilnehmenden zeigt mögliche Verbesserung
durch Erinnerungs-Apps. *Grenze:* überwiegend ältere Teilnehmende, viel Selbstbericht,
Übertragbarkeit auf Elvanse und Escitalopram mäßig.

### 9.5 Beschwerden — Stufe B

Clarsen B, Myklebust G, Bahr R (2013). *Development and validation of a new method for the
registration of overuse injuries in sports injury epidemiology: the OSTRC overuse injury
questionnaire.* Br J Sports Med 47(8):495–502.
DOI [10.1136/bjsports-2012-091524](https://doi.org/10.1136/bjsports-2012-091524) (PMID 23038786).
Über PubMed geprüft. 13 Wochen, 313 Athletinnen und Athleten aus fünf Sportarten, Handball
dabei. Zentrales Ergebnis: die Standardregistrierung erfasste nur 40 Überlastungsverletzungen,
das neue Verfahren 419 Probleme, davon 142 substanziell. Wöchentlich berichteten im Schnitt
39 % Beschwerden, 13 % substanzielle.

Hirschmüller A, Steffen K, Fassbender K, et al. (2017). *German translation and content
validation of the OSTRC Questionnaire.* Br J Sports Med 51(4):260–263.
DOI [10.1136/bjsports-2016-096669](https://doi.org/10.1136/bjsports-2016-096669) (PMID 27797733).
Cronbachs α 0,92, ICC 0,91.
*Grenze, die in der App genannt wird:* validiert an **24 Paralympics-Athletinnen und -Athleten**
über 20 Wochen. Das ist eine schmale und spezielle Basis — der Quellenkatalog V1 beschreibt sie
zu allgemein als „deutschsprachige strukturierte Erfassung".

Vier Fragen mit je 0/8/17/25 Punkten, Summe 0–100. Die App zeigt den Verlauf und bewertet ihn
nicht. Sie stellt keine Diagnose und ersetzt keine Untersuchung.

### 9.6 Worauf Prävention zielt — Stufe B, mit ausdrücklichem Widerspruch

Vila H, Barreiro A, Ayán C, et al. (2022). *The Most Common Handball Injuries: A Systematic
Review.* Int J Environ Res Public Health 19(17):10688.
DOI [10.3390/ijerph191710688](https://doi.org/10.3390/ijerph191710688) (PMID 36078403).
27 Studien: häufigste Lokalisationen sind untere Extremität (Oberschenkel, Knie, Sprunggelenk)
und Schulter; die meisten Verletzungen entstehen im Wettkampf. Rückraumspieler über der
6-Meter-Linie sind besonders betroffen.

**Der Widerspruch, den die App offen benennt:** Yonneau J, Lefèvre-Colau MM, Compagnat M, et al.
(2025). *Shoulder injuries prevention programmes in handball: a systematic review with
meta-analysis.* BMJ Open Sport Exerc Med 11(3):e002416.
DOI [10.1136/bmjsem-2024-002416](https://doi.org/10.1136/bmjsem-2024-002416) (PMID 41035524).
Fünf eingeschlossene Arbeiten mit 1.872 Spielenden, aber nur **drei** in der Meta-Analyse
(n=747): **OR 0,73; 95 %-KI 0,45–1,17 — kein statistisch gesicherter Effekt.**

Konsequenz: multimodale Prävention ja, Schultergarantie nein. Die App verspricht für die
Schulter ausdrücklich nichts.

Zum Trainingsinhalt bleibt die Lage gut: Bragazzi NL, Rouissi M, Hermassi S, Chamari K (2020),
*Resistance Training and Handball Players' Isokinetic, Isometric and Maximal Strength, Muscle
Power and Throwing Ball Velocity.* Int J Environ Res Public Health 17(8):2663.
DOI [10.3390/ijerph17082663](https://doi.org/10.3390/ijerph17082663) (PMID 32294971) —
18 Studien, 275 Spieler, Gesamteffekt 1,00 (95 %-KI 0,83–1,17), Wurfgeschwindigkeit 1,36,
Maximalkraft 1,82; isokinetische Kraft dagegen **nicht** signifikant (0,08).
*Grenze:* hohe Heterogenität und Hinweise auf Publikationsbias — von den Autoren selbst benannt.

Wang X, Zhang K, Samsudin SB, et al. (2024), *Effects of Plyometric Training on Physical Fitness
Attributes in Handball Players.* J Sports Sci Med 23(1):177–195.
DOI [10.52082/jssm.2024.177](https://doi.org/10.52082/jssm.2024.177) (PMID 38455436) —
20 Studien, 563 Spielende. Sprung mit Armschwung 1,84, Agilität −1,60, Maximalkraft 0,52.
**Balance wurde nicht verbessert.** Programme über acht Wochen wirkten auf Sprint deutlich
stärker als kürzere.

Alle sechs Arbeiten dieses Abschnitts wurden über PubMed abgerufen und die Zahlen gegen die
Abstracts geprüft, nicht aus einer Sekundärquelle übernommen.

### 9.7 Finanzieller Impulsschutz — Stufe B für das Prinzip, D für die Zahlen

Gestützt ist die Strategieklasse: eine Meta-Analyse über 29 Experimente zu finanziellen
Selbstkontrollstrategien (Budgets, Sparautomatik, Zugriffshürden) und die ökonomische
Übersichtsarbeit zu Commitment Devices. *Grenze:* hohe Heterogenität, Wirkung stark
kontextabhängig.

Der Zusammenhang zwischen ADHS und schwierigeren Finanzentscheidungen ist in
Beobachtungsstudien gezeigt (u. a. n=1.292 Gemeindestichprobe; 225 ADHS gegen 121 Vergleich zu
Kaufimpuls und Belohnungsaufschub). *Grenze:* Korrelation, Selbstbericht, und **keine einzige
geprüfte ADHS-Finanz-App.**

**Nicht gestützt sind die konkreten Zahlen.** Die 40-Euro-Grenze und die 21-Uhr-Regel sind
Maiks persönliche Schutzregeln. Die 24-Stunden-Wartezeit stammt aus Erfahrungsberichten und ist
eine runde Zahl, kein Messergebnis. In der App als Stufe D gekennzeichnet und frei einstellbar.

### 9.8 Was diese App als Web-App nicht kann

Kein Quellenbeleg nötig, sondern Plattformdokumentation — und die wichtigste Einschränkung
des ganzen Masterplans:

- **Exact Alarms** (`android.developer.android.com/develop/background-work/services/alarms`),
  **Full-screen intents** (Android-14-Verhaltensänderungen) und geplante Vibration sind native
  Android-Schnittstellen. Eine Seite im Browser erreicht sie nicht, mit keiner Berechtigung.
- **Health Connect** ist eine Android-Schnittstelle für native Apps. Gleiches gilt für Samsung
  Health und Huawei Health.
- **Geofencing** für ortsbezogene Erinnerungen: nativ.
- **Web Push** bräuchte einen eigenen Server und wird von Android zusätzlich gedrosselt.

Die in Masterplan V8 beschriebene eskalierende Erinnerungsleiter — Ton, Vibration, dauerhaft
sichtbare Karte, Zwei-Stunden-Vorlauf — ist damit **in dieser Architektur nicht baubar**. Der
Masterplan zitiert die Android-Dokumentation korrekt, zieht aber nicht die Konsequenz, dass er
dafür eine native App verlangt.

Pivot baut deshalb auf Kontextankern (nach dem Essen, beim Heimkommen, vor dem Aussteigen) und
auf dem Google Calendar, in dem Maik ohnehin lebt. Änderbar wäre das nur über einen
Capacitor-Wrapper mit Android Studio und Signaturschlüssel — ein eigenes Projekt.
