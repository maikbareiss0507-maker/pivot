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

---

## 10. Reflexion und Notfallknopf (ab V5.2)

### 10.1 Aufbau der Reflexion — Stufe C

Der Ablauf (Stimmung, Gefühle, Körperempfindungen, Kontext, Freitext) ist von Liven übernommen,
weil Maik damit arbeiten konnte und mit der vorherigen Drei-Fragen-Fassung nicht. Das ist eine
Produktentscheidung nach Gebrauchstauglichkeit, kein Wirksamkeitsbeleg — und wird in der App
auch nicht als solcher dargestellt.

Was dahintersteht: Stimmungsmonitoring kann nützen, erzeugt aber auch Belastung; die vorhandene
systematische Übersicht dazu untersuchte bipolare Störung, nicht ADHS oder Depression direkt.
Deshalb bleibt die Reflexion freiwillig, mehrmals täglich möglich und ohne Pflichtcharakter.

**Die Musterkarte erscheint erst ab acht Einträgen** und benennt ausdrücklich, dass Häufigkeiten
keine Ursachen sind. Was oft gemeinsam auftritt, muss einander nicht auslösen.

### 10.2 Notfallknopf bei Drang — Stufe C

**Wichtiger Befund vorab.** Die Konsensusarbeit der International Society for Sexual Medicine
zu Compulsive Sexual Behavior Disorder benennt als eigenständiges Problem unter anderem:
Selbstetikettierung, lustfeindliche Haltungen, das Vermischen normativer Einstellungen mit
klinischem Leidensdruck und ausdrücklich „the belief that masturbation and pornography use
represent 'unhealthy' sexual behavior".

Briken P, Bőthe B, Carvalho J, et al. (2024). *Assessment and treatment of compulsive sexual
behavior disorder: a sexual medicine perspective.* Sex Med Rev 12(3):355–370.
DOI [10.1093/sxmrev/qeae014](https://doi.org/10.1093/sxmrev/qeae014) (PMID 38529667).
Über PubMed geprüft.

Daraus folgt für die App: **kein Zähler, keine Serie, kein Protokoll, keine Zielvorgabe.** Der
Knopf speichert nichts — das ist im Testlauf byteweise geprüft. Er endet ausdrücklich damit,
dass es kein Scheitern gibt, wenn es trotzdem passiert. Und er ist bewusst für *jeden* Drang
gebaut, nicht für ein einzelnes Verhalten: die Handgriffe sind dieselben, und ein Werkzeug, das
nur für ein Verhalten existiert, wird selbst zum Etikett.

Zur Behandlungslage insgesamt: Antons S, Engel J, Briken P, et al. (2022), *Treatments and
interventions for compulsive sexual behavior disorder with a focus on problematic pornography
use: a preregistered systematic review.* J Behav Addict 11(3):643–666.
DOI [10.1556/2006.2022.00061](https://doi.org/10.1556/2006.2022.00061) (PMID 36083776).
24 Studien, davon **nur 4 randomisiert kontrolliert**; die beste Evidenz besteht für kognitive
Verhaltenstherapie. *Grenze:* die Autoren mahnen ausdrücklich zur Zurückhaltung bei Aussagen
über die Spezifität der Behandlungen.

**Schritt 1 — Reizkontrolle (Ort wechseln).** Grundbestandteil verhaltenstherapeutischer
Rückfallprävention. Kein eigener Wirksamkeitsbeleg für diesen konkreten Handgriff; als Prinzip
in der CBT-Literatur zu Suchtverhalten durchgehend enthalten.

**Schritt 2 — 90 Sekunden moderate Bewegung.** Der am konkretesten belegte Handgriff:
Kurti AN, Dallery J (2014). *Effects of exercise on craving and cigarette smoking in the human
laboratory.* Addict Behav 39(6):1131–7.
DOI [10.1016/j.addbeh.2014.03.004](https://doi.org/10.1016/j.addbeh.2014.03.004) (PMID 24656643).
Über PubMed geprüft. Nach moderater Bewegung verlängerte sich die Zeit bis zum nächsten
selbstgewählten Rauchen von im Mittel **4 auf 21 Minuten**; der Effekt lief über die
Belohnungskomponente des Verlangens, nicht über die Entzugskomponente.
*Grenze:* Laborstudie mit 20 beziehungsweise 21 Teilnehmenden, Rauchen als Zielverhalten.
Die Übertragung auf andere Dränge ist plausibel, aber nicht geprüft.

Garey L, Thai JM, Zvolensky MJ, Smits JAJ (2024). *Exercise and Smoking Cessation.*
Curr Top Behav Neurosci 67:177–198.
DOI [10.1007/7854_2024_497](https://doi.org/10.1007/7854_2024_497) (PMID 39090290).
Robuste Evidenz für die Reduktion von Verlangen, Entzugssymptomen und negativem Affekt;
kurzfristige Abstinenz verbessert, langfristige eher nicht.

**Schritt 3 — neu entscheiden.** Kein Wirksamkeitsbeleg für die Formulierung. Was hier
ausdrücklich *nicht* behauptet wird: dass Achtsamkeit den Drang zuverlässig auflöst.
Grant S, Colaiaco B, Motala A, et al. (2017), *Mindfulness-based Relapse Prevention for
Substance Use Disorders.* J Addict Med 11(5):386–396.
DOI [10.1097/ADM.0000000000000338](https://doi.org/10.1097/ADM.0000000000000338) (PMID 28727663).
9 RCTs, 901 Teilnehmende: **kein signifikanter Unterschied beim Rückfall** (OR 0,72;
95 %-KI 0,46–1,13), nur kleine signifikante Effekte auf Verlangen und Entzug
(SMD −0,13; KI −0,19 bis −0,08) und auf negative Folgen (SMD −0,23). Evidenzqualität niedrig.

Das heißt konkret: „Den Drang aushalten" ist keine belegte Methode, um die Handlung zu
verhindern. Die Ortsveränderung und die Bewegung sind die Teile mit Substanz.

### 10.3 Was die App hier nicht tut

Sie stellt keine Diagnose, sie bewertet kein Sexualverhalten als gesund oder ungesund, und sie
zählt nichts mit. Wenn Leidensdruck bestehen bleibt, ist die belegte Adresse
Verhaltenstherapie — nicht eine App und nicht ein Ratgeber aus einem Forum.

---

## 11. Vier-Wochen-Reset in der App (ab V5.3)

Alle Inhalte dieses Bereichs stammen aus Maiks eigenem Dokument „Vier Wochen Reset für
Sexualität und Rauchen" (Stand 14.06.2026). Die App macht daraus bedienbare Knöpfe und
erfindet nichts dazu. Die Evidenzeinordnung des Dokuments wird übernommen, nicht überschrieben:

- **Gut belegt:** Sexualnebenwirkungen von Lisdexamfetamin und Escitalopram; Rauchen,
  Bewegungsmangel, Schlafprobleme und Depression/Angst als ED-Risikofaktoren (EAU-Leitlinie);
  Leistungsdruck und kognitive Selbstbeobachtung als Störfaktoren.
- **Schwach bis gemischt:** der Zusammenhang „Pornos verursachen ED". Für bloße Nutzungsfrequenz
  findet sich meist keine konsistente kausale Verbindung; problematisch erlebte Nutzung ist
  häufiger querschnittlich assoziiert.
- **Plausibel, nicht hart bewiesen:** dass das enge Solo-Erregungsmuster schlechter zu
  Partnersex passt. Die klinische Literatur zu idiosynkratischem Masturbationsstil beschreibt
  das vor allem bei verzögerter Ejakulation.
- **ADHS ist kein direkter ED-Auslöser**, erhöht aber die Relevanz von Reizkontrolle, Routinen
  und externen Hilfen.

### 11.1 Notfallknopf — Abschnitt 5.2 des Plans

Der Knopf zeigt **eine** Option, beim nächsten Druck eine andere. Grundlage ist Maiks eigene
„ADHS-Notfallliste für schnelles Dopamin", erweitert um Optionen aus seinen echten App-Daten
(offene Aufgabe, nächster Haushaltsschritt, laufendes Essensfenster, Eintrag aus dem Eingang).

Leitsatz aus dem Plan, der die Gestaltung bestimmt: *„Der Punkt ist nicht perfekte Achtsamkeit,
sondern sofortige Verhaltensunterbrechung. Das ist bei ADHS meist wirksamer als langes
Nachdenken."*

Deshalb: **kein Zähler, keine Serie, kein Protokoll.** Im Testlauf wird byteweise geprüft, dass
der Zustand vor und nach einem Durchlauf identisch ist. Belegt sind von den angebotenen
Handgriffen vor allem Ortswechsel (Reizkontrolle, CBT-Standard) und moderate Bewegung
(Kurti & Dallery 2014: Verlängerung von 4 auf 21 Minuten bis zum nächsten selbstgewählten
Rauchen, siehe Abschnitt 10.2). Für die übrigen Optionen gilt: plausibel, nicht einzeln geprüft.

### 11.2 Rauchslots — Abschnitt 6 des Plans

Fünf feste Slots (A Morgen nach dem Frühstück, B Mittag, C Feierabend, D nach dem Abendessen,
E Flex für genau einen starken Trigger). Die App zählt weiter, aber die Kennzahl, die sie
hervorhebt, ist die **Zahl der Zigaretten außerhalb eines Slots** — entsprechend dem Leitsatz
„Zigarette nur im Slot, nie im Impuls".

Hintergrund aus dem Plan: Die erste Zigarette kurz nach dem Aufstehen ist ein starker Marker
für Nikotinabhängigkeit; deshalb Slot A frühestens 45–60 Minuten nach dem Aufstehen und nach
dem Frühstück. NICE betont ausdrücklich, dass jedes Rauchen schadet — die Reduktion auf fünf
ist ein Zwischenschritt zur Kontrolle, kein gesundheitlich unbedenkliches Ziel.

### 11.3 Wenn-dann-Pläne, Situationen, Rückfallplan — Abschnitte 5.1, 5.3, 8.2

Übernommen wie im Dokument. Der Rückfallplan trägt die wichtigste Regel daraus:
**kein Kettenrückfall aus Kränkung.** Der zerstörerische Gedanke ist nicht „ich bin
gescheitert", sondern „jetzt kann ich auch komplett drauf pfeifen".

### 11.4 Arzt-Checkliste — Abschnitt 8.3

Wörtlich übernommen. Die App ändert keine Dosis, empfiehlt kein Präparat und rät nicht zum
Absetzen. Elvanse, Escitalopram, wiederkehrende Erektionsprobleme und Potenzmittel gehören
nach dem Plan selbst ausdrücklich nicht in Selbstexperimente.

---

## 12. Regeneration (ab V5.4)

Der gesamte Regenerationsbereich stammt aus Maiks geprüftem Abschlussbericht
**„Evidenzbasierte Regeneration für Handballspieler"** (04.–05.09.2026, 114 Quellen, zwei
unabhängige Prüfrunden, Urteil BESTANDEN). Der vollständige Bericht liegt als `REGENERATION.md`
im selben Ordner; die Verweise in eckigen Klammern zeigen auf dessen Quellenliste.

Die App übernimmt die Vier-Gruppen-Einordnung aus Abschnitt 19b unverändert und weicht sie
nirgends auf.

### 12.1 Die Aussage, die den Aufbau bestimmt

> Das Wirksame sieht nicht nach Regeneration aus. Schlaf, Essen, Trinken und vernünftige
> Belastungssteuerung haben über alle gemessenen Endpunkte die mit Abstand breiteste Evidenz.
> Eisbad, Sauna, Faszienrolle, Massage und Wechselbäder haben kleine, oft nur subjektive und
> teils gegensätzliche Effekte.

Deshalb stehen Trinken, Mahlzeit, Casein, Koffeinkarenz und Schlafrhythmus als **fest** in der
App — und Rolle, Massage, Wechselbäder als **optional** weiter unten. Nicht umgekehrt.

### 12.2 Kälte ist kontextabhängig, nicht gut oder schlecht

- **Nach dem Spiel vertretbar:** senkt das Muskelkatergefühl (g ≈ −0,40 bis −0,66) und CK [1, 3, 15].
- **Nach dem Krafttraining nicht:** dämpft die langfristige Kraftanpassung
  (SMD −0,60 bzw. ES −0,23 in zwei Metaanalysen) [2, 4, 6, 93].
- **Nicht direkt vor Sprung- oder Sprintbelastung:** Sprungkraft danach schlechter
  (g ≈ −0,68 bis −0,94) [2, 17].

**Umsetzung:** Kaltwasser erscheint ausschließlich an Spieltagen. An Krafttagen erscheint
stattdessen ein eigener Block „Heute ausdrücklich nicht" mit der Begründung und der Effektgröße.
Dieser Negativblock ist der Teil, den ein Regenerationsplan sonst nie enthält.

### 12.3 Das warme Bad, nicht das kalte

Die bestbelegte Anwendung der Badewanne ist ein **warmes Bad, 40–42,5 °C, mindestens 10 Minuten,
ein bis zwei Stunden vor dem Schlafengehen** — metaanalytisch bessere Schlafqualität [24].
Es steht an Team- und Spieltagen sowie an freien Tagen als fester Punkt.

### 12.4 Für Maik fest gesetzt

Nach seinen Angaben vom 08.09.2026: Sprunggelenk eingeschränkt, Schienbein gerade ruhig.

- **Mobilityblock Wade und Sprunggelenk** als eigene Einheit, nicht als Anhängsel [32, 112].
- **Neuromuskuläres Training** — der einzige Punkt im gesamten Bericht mit GRADE **hoch**:
  senkt das MTSS-Risiko, 12 RCTs, 8197 Teilnehmende [99]. Das ist **Vorbeugung, nicht
  Behandlung**.

**Offener Widerspruch, den die App nicht glättet:** Für die *Behandlung* eines bestehenden
Schienbeinkantensyndroms stehen Dehnen und Kräftigen ausdrücklich auf der Negativliste [98, 100].
Das kollidiert mit dem, was für die Sprunggelenksmobilität sinnvoll wäre. Solange das Schienbein
ruhig ist, greift die Präventionsseite; wird es akut, gilt die Gegenaussage.

### 12.5 Zwei Fragen, die die App nicht beantwortet

- **Sauna unter Elvanse und Escitalopram.** Die gesamte akute Evidenz zur klassischen Sauna nach
  dem Training beruht auf **einer einzigen Studie mit negativem Ergebnis** [21]. Zusammen mit der
  ungeklärten Medikationsfrage gibt es keine Grundlage für eine Empfehlung — weder dafür noch
  dagegen. Die App zeigt beides und einen Haken „mit der Ärztin geklärt".
- **Zusätzliches Koffein neben Lisdexamfetamin.** Dazu existiert keine verwertbare Literatur.
  Die Karenzzeit von 8,8 Stunden für 107 mg [44] gilt unabhängig davon für den Schlaf.

### 12.6 Umbau in V5.5 — warum die erste Fassung unbrauchbar war

Die erste Fassung stand als eigener Bereich unter „Mehr" und schrieb Effektgrößen, GRADE-Stufen
und Fachbegriffe direkt auf die Karten. Maiks Rückmeldung: unübersichtlich, zu viele Fachbegriffe,
und nirgends steht einfach, was zu tun ist. Das war zutreffend.

**Regel für diesen Bereich seitdem:** An der Oberfläche steht, WAS zu tun ist, in normalen Worten.
Zahlen, Effektgrößen, Studiendesigns und Fachbegriffe stehen ausschließlich hinter dem
Fragezeichen. Ein automatischer Test durchsucht die Oberfläche auf die Begriffe SMD, GRADE, MTSS,
PNF, Casein, Immersion, Homöostase, Hedges, neuromuskulär, Mobility und metaanalytisch — findet er
einen davon, schlägt der Test fehl.

Beispiele für die Übersetzung:

| Vorher | Jetzt an der Oberfläche |
|---|---|
| Casein 30–40 g vor dem Schlafen | Quark-Shake vor dem Schlafen — ungefähr 250 g Magerquark mit einem Löffel Proteinpulver |
| Neuromuskuläres Training | Balance und Landungen üben — einbeinig stehen, von der Bank springen und weich landen |
| Mobility Wade und Sprunggelenk | Waden und Sprunggelenk dehnen — Wade am Türrahmen, Knie über die Zehen schieben |
| Kaltwasserimmersion | Kalt baden |
| Dynamisches Aufwärmen | Aufwärmen in Bewegung — locker einlaufen, Arme kreisen, nichts lange halten |
| Mahlzeit mit 20–32 g Protein | Iss was Richtiges — Hähnchen mit Reis, Linsen mit Brot, Nudeln mit Quark |

**Struktur:** Regeneration ist keine eigene Kachel mehr, sondern eine Nebeneinheit im
Training-Reiter neben „Einheiten" und „Last". Die Seite zeigt in dieser Reihenfolge:
Pflicht, Heute nicht, Optional. Wochenplan, Ausstattung und Kalenderexport sind eingeklappt,
damit die Seite oben aufhört.

Schlafrhythmus, Quark-Shake und Koffeinkarenz gelten an **jedem** Tag — auch an Trainertagen und
am Tag nach dem Spiel. In der ersten Fassung fielen sie dort stillschweigend weg.

### 12.7 Feste Termine über den Kalender

Die App erzeugt eine `.ics`-Datei mit den festen Wochenblöcken für vier Wochen (Mobility und
neuromuskuläres Training Dienstag und Donnerstag, warmes Bad Montag und Mittwoch abends). Das
ist der einzige Weg, wie eine Web-App verlässlich erinnern kann — siehe Abschnitt 9.8.
Vier Wochen deshalb, damit der Kalender nicht mit einem Rhythmus zugestellt wird, der sich
ändert.

Jeder Termin enthält **nur den Inhalt dieses Tages** als kurze Handlungsschritte, kein Verweis
auf ein anderes Dokument und keine Fachbegriffe — zum Beispiel „Wade am Türrahmen dehnen, 3 mal
30 Sekunden pro Seite". Dehnen und Balance sind getrennte Termine mit eigener Kategorie, damit
sie im Kalender unterschiedlich eingefärbt werden können. Ein Test prüft das Format der Datei
und dass keiner der gesperrten Fachbegriffe darin vorkommt.

---

# 13 · V5.6 — Prüfung durch das App Engineering Studio

Vier unabhängige Prüfagenten haben den Ist-Zustand von V5.5 durchgesehen: Produkt und
Anforderungen, Design und Bedienbarkeit, Sicherheit und Datenschutz, Recht. Die Befunde
wurden reproduziert, bevor sie behoben wurden. Was hier steht, ist geprüft — nicht behauptet.

## 13.1 Nutzertext in `onclick` war ausführbarer Code

**Der Befund.** An acht Stellen wurde Text, den Maik selbst eingetippt hat — Aufgabentitel,
Wunschtitel, Einkaufsposten, eigene Begriffe in der Reflexion, Trainingsauslöser — direkt in
ein `onclick`-Attribut geschrieben. Abgesichert war das mit `esc()` und einem
`.replace(/'/g,'')`. Beides genügt nicht.

**Warum es nicht genügt.** Der HTML-Parser dekodiert Zeichenreferenzen im Attributwert,
**bevor** der Browser den Inhalt als JavaScript liest. Aus dem `&#39;`, das `esc()` erzeugt,
wird also wieder ein echtes Apostroph — und zwar genau rechtzeitig, um den String zu schließen.
Die Reihenfolge ist in der HTML-Spezifikation festgelegt (WHATWG HTML, *Attribute value
(single-quoted) state* → *Character reference state*), das ist kein Browserfehler.

**Der Nachweis.** Ein Eintrag mit dem Titel

    x'); window.__pwn=(window.__pwn||0)+1; //

setzt in V5.5 den Zähler `window.__pwn` — der Code läuft. Gegen V5.6 läuft er nicht.
Beide Fassungen wurden im selben Durchlauf auf zwei Ports gegeneinander gehalten
(`/tmp/build/xss.js`, `/tmp/build/xss-alt.js`): V5.5 „AUSNUTZBAR" auf allen drei Vektoren,
V5.6 „dicht" auf allen drei.

**Was das praktisch bedeutete.** Die App liegt auf `github.io`. Alles, was in ihrem
Zusammenhang läuft, kann `localStorage` lesen — also Diagnosen, Medikation, Reflexionen,
Finanzen. Der Angriffsweg ist schmal, weil nur Maik selbst eintippt; er ist nicht null, weil
Backup-Dateien importiert werden können und ein `.json` aus fremder Hand denselben Weg nimmt.

**Die Behebung.** Nutzerdaten werden gar nicht mehr in Attribute geschrieben. Stattdessen legt
`A(wert)` den Wert in eine Liste und gibt einen Zahlenindex zurück; im Attribut steht nur noch
`$a(3)`. Zahlen können nicht ausbrechen. Die Liste wird bei jedem `render()` geleert.

## 13.2 Import und `deepMerge` waren nicht abgedichtet

`deepMerge` lief über `for(const k in b)` ohne Prüfung. Ein Backup mit dem Schlüssel
`__proto__` konnte damit Eigenschaften auf `Object.prototype` setzen, die dann an jedem
Objekt der App hängen. Zusätzlich übernahm `impo()` jedes Feld einer Backup-Datei,
auch unbekannte.

Behoben: `__proto__`, `constructor` und `prototype` werden übersprungen, geerbte Schlüssel
ebenfalls, und der Import lässt nur noch Felder durch, die in `DEF` vorkommen.

## 13.3 Inhaltssicherheitsregel (CSP)

Neu ist eine `Content-Security-Policy` im Kopf der Seite. Sie erlaubt Netzverbindungen nur
noch zu `world.openfoodfacts.org` — der einzigen Fremdadresse, die die App braucht. `object-src
'none'` und `base-uri 'none'` schließen zwei ältere Umleitungswege.

Geprüft mit `/tmp/build/csp.js`: eine untergeschobene Anfrage an `https://fremd.example` wird
blockiert, der Barcode-Abruf läuft weiter. `'unsafe-inline'` bleibt für Skript und Stil nötig,
weil die App bewusst aus einer einzigen Datei besteht; die CSP ist damit kein Ersatz für 13.1,
sondern die zweite Reihe dahinter.

## 13.4 Medikamentenwarnung erlosch bei Bestand null

    warn: s>0 && s<=(it.puffer||7)     // vorher
    warn: s<=(it.puffer||7)            // jetzt, plus eigene Meldung „Bestand ist leer"

Bei Bestand 0 war `s>0` falsch, also verschwand die Nachbestellwarnung — in dem Moment, in dem
sie am nötigsten ist. Ein Test prüft jetzt die Bestände 0, 1, 7, 8 und den nie erfassten Fall.

## 13.5 Bereitschaftswert war rot eingefärbt

Ein roter Wert liest sich wie ein Befund. Die Bereitschaft ist aber nur ein Vergleich mit dem
eigenen 14-Tage-Schnitt und kein Gesundheitswert — genau das, wovor Impellizzeri 2020 bei
abgeleiteten Belastungskennzahlen warnt. Rot ist jetzt Blau, und unter dem Wert steht die
Einordnung im Klartext.

## 13.6 Haushaltskachel zeigte den Rückstand

Die Kachel meldete bis zu zehn offene Aufgaben. Eine zweistellige Rückstandszahl auf der
Startseite ist genau die Wand, die die App vermeiden soll (Abschnitt 12.2). Sie zeigt jetzt
höchstens eine — die nächste.

## 13.7 Zugänglichkeit

- `maximum-scale=1` entfernt. Es unterband das Zoomen und verstößt gegen WCAG 2.2, 1.4.4.
- Antippbare Flächen auf mindestens 24 × 24 px vergrößert (WCAG 2.2 AA, 2.5.8): `.qm` 17 → 26,
  `.rq` 22 → 30, `.tick` 28 → 32, `.rtick` 26 → 30, `.x` und die kleinen Knöpfe entsprechend.
  **Nicht** über eine unsichtbare Vergrößerung gelöst — das hätte Tipper von den umliegenden
  Karten weggefangen, weil `.qm` in `.rcard` sitzt und `.rcard` selbst ein Knopf ist.
- Kontrast der Hilfstexte angehoben: dunkel `#6b7789` → `#8996a8`, hell `#8391a4` → `#5f6c7e`.
  Damit über 4,5:1 (WCAG 2.2 AA, 1.4.3).
- Reiter tragen `aria-current="page"` und einen Namen, Kacheln einen Zweck, Zierzeichen
  `aria-hidden`.
- Der laufende Fokus-Zeitalarm ließ sich nicht mehr durch einen Tipp daneben abbrechen.

## 13.8 Was bewusst nicht geändert wurde

Repo-Sichtbarkeit, das Entfernen von Namen oder persönlichen Passagen aus den Dateien und ein
Umschreiben der Git-Historie sind Entscheidungen von Maik, nicht von mir. Sie sind unumkehrbar
oder haben einen Preis (das Hosting), und ich habe dafür auch keinen Zugang.

---

# 14 · V5.7 — Zimmerplan, ein kritischer Speicherfehler, drei Alltagsfixes

## 14.1 KRITISCH: Neuladen löschte in V5.6 alle Eingaben

**Der Fehler.** In der Sicherheitsrunde V5.6 kamen `const GIFT` und die abgesicherte
`deepMerge`-Funktion in den Code — aber **unterhalb** der Zeile `let S = load()`. `deepMerge`
ist als Funktion hochgezogen und damit früh aufrufbar, `GIFT` als `const` jedoch nicht: bis zu
seiner eigenen Zeile liegt es in der temporalen Totzone. `load()` rief `deepMerge` also auf,
`deepMerge` griff auf `GIFT` zu, das warf einen `ReferenceError`, und der `try/catch` in `load()`
fing ihn stumm ab und gab die **Standardwerte** zurück. Ergebnis: bei jedem echten Neuladen der
Seite wurde der gespeicherte Zustand durch die Defaults ersetzt und diese anschließend
zurückgeschrieben.

**Warum es niemandem auffiel.** Der Import einer Sicherungsdatei ruft dieselbe `deepMerge`, läuft
aber später — `GIFT` ist dann längst initialisiert. Import funktionierte also, und eine PWA lädt
im Alltag selten wirklich neu (sie bleibt im Speicher). Der Fehler schlug nur beim harten
Neuladen zu.

**Reichweite.** Der Fehler existierte ausschließlich in den V5.6-Dateien, die noch **nicht**
veröffentlicht waren. Die live genutzte Fassung ist V5.5 und kennt `GIFT` nicht — sie ist nicht
betroffen. Der Fehler wurde vor jeder Auslieferung gefunden.

**Behebung.** `GIFT` und `deepMerge` stehen jetzt **vor** `let S = load()`. Ein Dauertest
schreibt Gewicht, Rauchprotokoll und einen Modulzustand, lädt die Seite neu und prüft, dass alles
noch da ist. Regel daraus: Was `load()` beim Start braucht, muss oberhalb von `load()` definiert
sein — hochgezogene Funktionen täuschen hier, weil ihre `const`-Abhängigkeiten es nicht sind.

## 14.2 Zimmerplan als Nebeneinheit im Haushalt

Aus der Übergabe-Spezifikation vom 09.09.2026 (25 Fotos, Obsidian, belegte Recherche): 35
Schritte für genau Maiks Zimmer, zehn Bereiche A–J in fester Reihenfolge, Strom und Kabel zuerst
(einziger Punkt mit echtem Risiko), Reinigen zuletzt. Umsetzung nach den ADHS-Regeln der App:

- Immer nur **ein** nächster Schritt sichtbar, nie die 35er-Liste zuerst.
- „Fertig" zählt auch bei nicht voll gesetzten Haken (Perfektionismusfalle vermeiden); teilweise
  wird als teilweise gespeichert.
- Die kurze Fassung zählt genauso wie die lange.
- 15–17 Uhr zeigt die App nur die kurze Fassung mit Hinweis aufs Tief.
- Ab 22:30 tritt die Abendrunde an die Stelle des nächsten großen Schritts.
- Wochenrunde Donnerstag nach dem Lernblock, Ersatz Sonntag.
- **Keine Serie, kein Zähler in Folge** — nur „zuletzt vor X Tagen". Ein ausgelassener Tag ist
  ausgelassen, nicht verloren.
- „Wohin damit?" schlägt die 21 festen Orte nach. „Alle Bereiche" erlaubt, einen Bereich
  vorzuziehen; die Reihenfolge innerhalb eines Bereichs bleibt fest.
- Medikamente werden nie zum Wegwerfen vorgeschlagen, das private Fach heißt neutral „Privates".

Läuft der Zimmerplan, klappt der generische Haushalt (Zonen, Grundreset, Rhythmen, feste Orte,
Tipps) hinter „Sonstiger Haushalt" ein — sonst liefe die Seite über, dieselbe Überfrachtung, die
bei der Regeneration bemängelt wurde.

Belege der Spezifikation (Implementation Intentions Gollwitzer & Sheeran 2006; Elektrosicherheit
VDE; Sturzunfälle DGUV 2023; Gewohnheitsbildung Lally 2010; kein Timer-Zwang nach Ergün 2025;
ausdrücklich nicht verwendet die Fehlzitation McMains & Kastner 2011) sind in der Spezifikation
selbst dokumentiert und werden hier nicht doppelt geführt.

## 14.3 Android-Zurück warf aus der App

Maik: „zurück knopf auf dem handy schmeißt mich aus der app". Eine PWA ohne eigene
Verlaufseinträge hat nichts, wohin sie zurückgehen könnte — Android schließt sie. Jeder Wechsel
in einen Bereich oder ein Fenster legt jetzt einen Verlaufseintrag an. Zurück schließt erst ein
offenes Fenster, geht dann zum Elternreiter, dann zur Startseite, und erst von dort hinaus. Zwei
Tests decken das ab.

## 14.4 Tagesrhythmus hing fest an 08:15

Maik: „wenn ich später aufstehe als vorgesehen, passt der tagesrythmus nicht mehr in der app".
Sein Export zeigt Einnahmen um 08:47, 11:42 und 13:10 — die Essensfenster hingen aber starr an
der geplanten Zeit 08:15. Jetzt gilt: ist für den Tag eine Einnahme eingetragen, verankern sich
alle Fenster und Phasen an der tatsächlichen Uhrzeit. Ohne Eintrag bleibt der Plan. Die Leiste
schreibt dann sichtbar „Einnahme 11:42 — Fenster verschoben".

## 14.5 Venenengel in die Regeneration aufgenommen

Aus dem Eingang: „für recovery wichtig ich habe einen venen engel zuhause." Als optionale Karte
aufgenommen, ehrlich eingeordnet: angenehm und unschädlich, aber ohne belegten Erholungsnutzen.
Eine PubMed-Suche am 10.09.2026 zu Beinhochlagerung und Erholung nach Belastung bei Sportlern
findet keinen passenden Treffer — das steht so auf der Karte. (Laut PubMed keine einschlägige
Studie; Suche dokumentiert, keine Quelle behauptet.)
