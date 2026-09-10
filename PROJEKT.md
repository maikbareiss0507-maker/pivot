# Pivot — Projektakte

Maiks Trainings-, Belastungs- und Ernährungs-App. Selbst gehostete PWA, läuft auf einem
Samsung Galaxy S23+ in Chrome. Alle Daten bleiben lokal auf dem Gerät.

## Entscheidungen

| Datum | Entscheidung | Begründung |
|---|---|---|
| 01.09. | Selbst gehostete PWA statt Artifact oder nativer App | Artifacts blockieren externe API-Aufrufe, damit wäre der Barcode-Scan tot. Native App bedeutet Play Store und Entwicklerkonto. |
| 01.09. | Daten in `localStorage`, kein Server, kein Konto | Keine Registrierung, keine Übertragung. Preis: Daten hängen an der Domain, deshalb JSON-Export. |
| 01.09. | Keine Ampel für die Acute:Chronic Workload Ratio | Methodisch widerlegt. Siehe QUELLEN.md, Abschnitt 4. |
| 02.09. | ADHS-Schicht vor Datenschicht und Trainingsplan-Modul | Die beste Datenschicht nützt nichts, wenn die App nicht benutzt wird. |
| 02.09. | Erinnerungen über den Kalender statt Web Push | Push bräuchte einen eigenen Server. Der Kalender existiert schon und Maik lebt darin. |
| 02.09. | Essen an Zeitanker statt an Hunger | Stimulanzien dämpfen den Appetit; Hunger ist als Auslöser unbrauchbar. |
| 02.09. | ~~Netlify bleibt der Host~~ — **überholt**, die App liegt auf GitHub Pages | Netlify erlaubt auf dem freien Plan nur etwa zwanzig Veröffentlichungen im Monat und pausiert die Seite danach. Preis des Wechsels: der Browserspeicher hing an der alten Domain. Ab jetzt gilt die GitHub-Pages-Adresse als feste Origin und darf nicht mehr wechseln. |
| 02.09. | Navigation bleibt Jetzt · Tag · Essen · Training · Mehr | Masterplan V8 schlägt Heute · Ernährung · Planung · Haushalt · Mehr vor. Das würde Training eine Ebene tiefer schieben, obwohl bessere Handballleistung das oberste Ziel ist. Haushalt sitzt als erste Kachel in Mehr — eine Berührung entfernt. |
| 02.09. | Keine eskalierende Erinnerungsleiter | Nicht "später", sondern in dieser Architektur unmöglich: Exact Alarms, Full-screen intents und geplante Vibration sind native Android-APIs. Halbgar vorgetäuscht wäre schlimmer als weggelassen. Siehe QUELLEN.md 9.8. |
| 04.09. | Ungenutzte Bereiche werden eingeklappt, nicht gelöscht | Nach drei Tagen ist „nie geöffnet" ein schwaches Signal — es kann an der Sache liegen oder daran, dass die Gelegenheit fehlte. Einklappen ist reversibel, Löschen nicht. |
| 04.09. | Kein Ausbau einzelner Bereiche in die Tiefe, obwohl Maik das gefordert hat | Seine Daten widersprechen der Forderung: der tiefste Bereich (Haushalt, 34 Schritte, 14 Anleitungen) hat null Taps, der flachste (Textfeld + Knopf) 25 Einträge. Tiefe ist nicht das Problem, fehlende Passung auf ihn ist es. Tiefe kommt pro Bereich und mit seinen Angaben, nicht geraten. |
| 02.09. | Nie erfasster Medikamentenbestand löst keine Warnung aus | Eine Warnung, die falsch losgeht, wird als erste ignoriert und nimmt allen echten Warnungen die Wirkung. |
| 02.09. | Evidenz an der Zahl statt in der Dokumentation | Wer nicht weiß, warum eine Zahl da steht, handelt nicht danach. Jede Kennzahl trägt Bedeutung, Quelle und Grenze bei sich. |
| 02.09. | Einnahmezeit bestätigt: 8:15 | Von Maik bestätigt, Kalendertermine passen. |
| 02.09. | Kein Streak-Zähler | Erhöhtes Delay Discounting bei ADHS macht ferne Belohnungen wirkungslos, und ein Aussetzer entwertet sonst alles Bisherige. |

## Aufbau

    index.html              komplette App, keine Abhängigkeiten, kein Build
    sw.js                   Service Worker — CACHE-Konstante bei jeder Änderung hochzählen
    manifest.webmanifest    macht die Seite installierbar
    icon-*.png              Homescreen-Icons
    QUELLEN.md              jede Formel mit Literaturstelle
    PROJEKT.md              diese Datei
    README.md               Hosting und Installation

## Stand

**Fertig**
- Kalorien per EAN-Scan über Open Food Facts, Plausibilitätsprüfung, Favoriten, manuelle Eingabe
- Handball- und Gym-Einheiten, Sätze mit kg/Wdh/RIR, e1RM nach Epley, Wochentonnage
- sRPE-Wochenlast, Monotonie, Strain, 7:28 ohne Ampel
- Tages-Check nach Hooper, Bereitschaft relativ zum eigenen 14-Tage-Schnitt
- ADHS-Schicht: Essensfenster am Einnahmeanker, Wenn-dann-Regeln, drei Hauptaufgaben mit
  kleinstem Start, Reparatur statt Streak, Heute-Ansicht auf eine nächste Handlung reduziert

**Fertig (02.09., zweite Sitzung)**
- Tagesleiste mit Weckzeit, Einnahme, Essensfenstern, Nachmittagstief und Jetzt-Marke
- Morgen- und Abendroutine zum Abhaken, plus Notfallversion für schlechte Tage
- Fokusfenster nach dem Training (Mehren et al. 2019, mit ausgewiesener Grenze)
- Startritual: zwei Minuten, mehr wird nicht verlangt
- „Warum?" an jeder Kennzahl — Bedeutung, Quelle und Grenze direkt an der Zahl

**Fertig (02.09., dritte Sitzung)**
- Mehrere benannte Mahlzeiten je Essensfenster, direkt auf der Heute-Ansicht antippbar
- Update-Hinweis nach einer neuen Version und Backup-Erinnerung nach sieben Tagen
- Speichern wird beim Wechsel in den Hintergrund sofort geschrieben (vorher 120 ms Verzögerung,
  eine Eingabe kurz vor dem Schließen konnte verloren gehen)

**Fertig (02.09., vierte Sitzung — Umbau nach Maiks Rückmeldung)**
- Navigation neu geschnitten: Jetzt · Tag · Essen · Training · Profil. „Last & Erholung" sitzt
  als Umschalter im Training-Tab statt als eigener Reiter.
- Startseite zeigt nur noch, was zur aktuellen Uhrzeit zählt. Sechs Tagesphasen (Nacht, Morgen,
  Vormittag, Nachmittagstief, Abend, Wind-down) bestimmen, welche Karten erscheinen.
- Aufgaben, Regeln, Routinen und Tagesleiste haben ihr eigenes Fenster im Tag-Tab.
- Essensfenster mit allen vier Mahlzeiten liegen im Essen-Tab; auf der Startseite steht nur das
  gerade laufende.
- Helleres, wärmeres Farbschema. Jeder Bereich hat eine eigene Farbe (Tag grün, Essen amber,
  Training blau, Profil violett), die Startseite färbt sich nach Tageszeit.

**Fertig (02.09., fünfte Sitzung — V5, Lebensbereiche aus Masterplan V8)**
- Navigation: fünfter Tab ist jetzt **Mehr**, ein stabiles Kachelverzeichnis mit zwölf
  Bereichen. Profil zog dorthin. Jetzt zeigt unten "Jetzt relevant" (höchstens drei
  kontextbezogene Kacheln) und "Alle Bereiche" als kompaktes Raster — nur Name, Symbol und
  offene Anzahl, nie Inhalte.
- **Haushalt**: Drei-Tage-Grundreset, vier Zonen mit geführter Reihenfolge, immer genau ein
  sichtbarer Schritt mit drei Reaktionen, Zeitgrößen 2/10/20–30 Minuten, Rettungsmodus,
  feste Orte, sieben Rhythmen inklusive Tierhaare, vierzehn Anleitungen, rotierender Textstil
  bei gleichbleibendem Aufgabennamen.
- **Fokus**: Timer von 2 bis 45 Minuten, Ablenkungsparkplatz mit Übergabe in den Eingang,
  stilles Body Doubling ohne Video und ohne Auswahl. Abschluss fertig / teilweise / anders.
- **Eingang**: universelle Erfassung über einen Schnellzugriff auf Jetzt und Tag.
- **Werkzeugkasten**: sechs Situationskarten mit je drei bis vier Handgriffen.
- **Medikamente**: Bestand mit Nachfüllpuffer, Einnahmebestätigung, Wochencheck (1–2 min),
  Zwei-Wochen-Rückblick (3–5 min), einmalige Serotonin-Sicherheitsinformation,
  Zusammenfassung zum Kopieren fürs Fachgespräch.
- **Finanzen**: Impulskauf-Check mit 40-Euro- und 21-Uhr-Regel, Wunschliste mit
  24-Stunden-Wiedervorlage, manuelle Töpfe, Fälligkeiten.
- **Beschwerden**: OSTRC-Logik mit vier Fragen und 0–100-Verlauf.
- **Reflexion**, **Zigarettenzähler mit Auslösern**, **Nullschritt-Drills**,
  **Wochenblick** mit Beziehungsanker und Bericht zum Kopieren.
- **Evidenzseite**: zwölf Quellenkarten mit Stufe A/B/C/D, Zielgruppe, Unsicherheit und der
  Frage, woran Maik nach zwei bis sechs Wochen merkt, ob es ihm hilft. Dazu sechs bekannte
  Widersprüche der Studienlage — statt dass die App sich eine Seite aussucht.
- Profilseite benennt ausdrücklich, was eine Web-App nicht kann.

**Fertig (04.09., sechste Sitzung — V5.1, nach Maiks Testlauf)**

Grundlage war sein Export vom 04.09., nicht sein Eindruck. Befund: fünf von zwölf Bereichen
in drei Tagen nie geöffnet (Haushalt, Finanzen, Reflexion, Drills, Beschwerden) — darunter
ausgerechnet der tiefste. Am meisten benutzt: Eingang und Ablenkungsparkplatz, 25 Einträge,
also das Flachste in der App. Konsequenz: nichts hinzugebaut, sondern aufgeräumt.

Vier bestätigte Fehler behoben:
- **Favoriten wurden nie gespeichert.** „Eintragen" legte keinen Favoriten an, nur der kleine
  Sternknopf daneben. Maik hat fünf Produkte gescannt und immer den grünen Hauptknopf gedrückt —
  `S.foods` blieb leer, jedes Produkt musste neu gescannt werden. Jetzt merkt sich die App jedes
  erfasste Produkt automatisch samt zuletzt benutzter Menge; der Sternknopf ist weg.
- **Scanner nahm den ersten Frame** mit irgendeinem Code, auch einen halb erfassten oder den
  Nachbarartikel. Jetzt muss derselbe Code dreimal hintereinander gelesen werden.
- **Tastatur ging beim Parken jedes Mal zu**, weil der ganze Sheet-Inhalt neu geschrieben wurde.
  Gleiches Problem im Eingang. Beide bleiben jetzt offen und fokussiert.
- **Beide Routinen immer aufgeklappt** im Tag-Reiter. Jetzt nur die fällige, die andere
  einzeilig und aufklappbar.

Weiter:
- Zigarettenzähler auf die Jetzt-Seite (ein Tap), 18 statt 8 Auslöser, **Mehrfachauswahl** —
  mehrere Auslöser treffen fast immer gleichzeitig zu. Zusammengesetzte Einträge werden in der
  Statistik einzeln gezählt.
- „Mehr" ist keine Symbolwand mehr, sondern eine Liste mit **Zweckzeile pro Bereich** (Maiks
  Frage „was macht der werkzeug kasten?" war berechtigt). Werkzeugkasten heißt jetzt
  „Wenn es klemmt".
- Bereiche sortieren sich selbst in „In Benutzung" und „Noch nicht benutzt". Nichts wird
  gelöscht; sobald Daten drin sind, wandert ein Bereich nach oben.
- **Helle Darstellung** als Umschalter im Profil, inklusive heller Tagesphasen-Farben.
- Der Bericht für Claude enthält jetzt Eingang und Ablenkungsparkplatz (bekannte Lücke aus V5).

**Fertig (04.09., siebte Sitzung — V5.1 bis V5.3)**

V5.1 behob vier bestätigte Fehler aus Maiks Testlauf (Favoriten wurden nie gespeichert, Scanner
nahm den ersten Frame, Tastatur schloss beim Parken, beide Routinen immer aufgeklappt), holte
den Zigarettenzähler auf die Jetzt-Seite, machte „Mehr" zur Liste mit Zweckzeile und brachte
die helle Darstellung.

V5.2 ersetzte die Drei-Fragen-Reflexion durch Livens Aufbau: Stimmung am Schieber, Gefühle,
Körperempfindungen, Kontext, Freitext — Mehrfachauswahl überall, eigene Begriffe ergänzbar,
mehrere Einträge pro Tag, Musterkarte erst ab acht Einträgen.

V5.3 baut Maiks eigenen Vier-Wochen-Reset ein:
- **Notfallknopf umgebaut** nach seiner Vorgabe: nicht drei feste Schritte, sondern **eine**
  Option aus rund dreißig, beim nächsten Druck eine andere. Vier davon kommen aus seinen echten
  Daten (offene Aufgabe, nächster Haushaltsschritt, laufendes Essensfenster, Eingangseintrag).
  Weiterhin kein Zähler, keine Serie, kein Protokoll — im Test byteweise geprüft.
- **Rauchslots A–E** statt reinem Zählen. Hervorgehobene Kennzahl ist die Zahl außerhalb eines
  Slots, nicht die Gesamtzahl.
- Sechs **Wenn-dann-Pläne** zum Übernehmen in die normale Regelliste, sechs **Situationen**,
  der **Rückfallplan** und die **Sätze für Evi** zum Antippen und Kopieren.
- **Arzt-Checkliste** für Elvanse, Escitalopram und Erektionsprobleme.

**Fertig (08.09., achte Sitzung — V5.4)**

Regenerationsbereich gebaut, vollständig aus Maiks geprüftem Abschlussbericht (114 Quellen,
zwei Prüfrunden, BESTANDEN). Der Bericht liegt als REGENERATION.md im Ordner.

- Der Plan richtet sich nach der **Tagesart**: erfasste Einheiten schlagen den Wochenrhythmus.
  Spiel, Krafttraining, Mannschaftstraining, Trainer-Tag, frei.
- **Fest / Optional / Zwischendurch** getrennt, wie von Maik gewünscht. Fest sind die Punkte
  mit breiter Evidenz (Trinken, Mahlzeit, Casein, Koffeinkarenz, Schlafrhythmus) — nicht
  Rolle und Sauna.
- Eigener Block **„Heute ausdrücklich nicht"**: an Krafttagen keine Kälte (SMD −0,60), keine
  Rolle vor Maximalkraft, kein langes statisches Dehnen davor.
- Für ihn fest gesetzt nach seinen Angaben: Mobility Sprunggelenk (eingeschränkt) und
  neuromuskuläres Training (Schienbein ruhig, Prävention hat GRADE hoch).
- Spieltag **Samstag/Sonntag/kein Spiel** in einem Tap umschaltbar, weil er wechselt.
- Ausstattung abwählbar — was er nicht hat, verschwindet aus dem Plan.
- Sauna mit ausdrücklichem ärztlichen Vorbehalt und Haken „geklärt".
- **Kalenderdatei** für die festen Wochenblöcke, vier Wochen im Voraus.

**Fertig (08.09., neunte Sitzung — V5.5, nach Maiks Rückmeldung)**

Seine Kritik an V5.4 war berechtigt: zu viele Fachbegriffe, keine einfachen Handlungsanweisungen,
unübersichtlich. Umgebaut:

- Regeneration ist **keine eigene Kachel mehr**, sondern eine Nebeneinheit im Training-Reiter
  neben „Einheiten" und „Last" — von Maik so festgelegt, nicht zur Diskussion gestellt.
- Der gesamte Text neu geschrieben: **an der Oberfläche steht, was zu tun ist**, in normalen
  Worten. Zahlen und Fachbegriffe nur noch hinter dem Fragezeichen. Ein Test durchsucht die
  Oberfläche auf elf gesperrte Begriffe und schlägt fehl, wenn einer auftaucht.
- Klarer Aufbau: **Pflicht** (große Karten) → **Heute nicht** → **Optional** (kleiner).
  Wochenplan, Ausstattung und Kalender eingeklappt.
- Kalendertermine enthalten jetzt **den Inhalt des jeweiligen Tages** als kurze Schritte,
  nicht den ganzen Plan und keinen Dokumentverweis. Dehnen und Balance getrennt mit eigener
  Kategorie, damit sie im Kalender unterschiedlich eingefärbt werden können.
- Fehler behoben: Schlafrhythmus, Quark-Shake und Koffeinkarenz fielen an Trainertagen und am
  Tag nach dem Spiel stillschweigend weg.

**Regel daraus, die bleibt:** Fachlich sauber heißt nicht, dass die Fachsprache auf dem
Bildschirm steht. Die Evidenz gehört hinter das Fragezeichen, die Handlung davor.

**Noch offen aus Maiks Kritik**
- Morgen- und Abendroutine: einzelne Schritte in Unterschritte zerlegen
- Ernährungsausbau — braucht von ihm Wochenbudget, Allergien, Kochmöglichkeiten
- Trainingszeiten sind noch angenommen, nicht bestätigt (siehe unten)

**Als Nächstes**
1. Wissenschaftliche Datenschicht — MET-Tabelle, Offline-Nährwerttabelle (USDA), Testbatterie
   mit Normwerten, Positionsprofil Rückraum, Mikronährstoff-Ampel
2. Trainingsplan-Modul — Sechs-Wochen-Zyklus mit Deload in Woche 4 und Tests in Woche 6,
   Autoregulation nach Bereitschaft
3. Ernährungs-Wochenplan, Rezepte, Vorräte, Einkaufsliste und Lebensmittelbudget aus
   Masterplan V8 Abschnitt F — der größte noch offene Block
4. Kalender Stufe eins: eigener lokaler Kalender in Pivot, danach erst OAuth zu Google
5. Spielprotokoll auf einer Körperkarte

**Offen**
- Schlaf und HRV automatisch importieren geht mit einer Web-App nicht. Huawei Fit 3 hat keine
  offene Schnittstelle, Health Connect ist für Web nicht zugänglich. Nur über einen
  Capacitor-Wrapper lösbar.
- Eskalierende Erinnerungen, ortsbezogene Erinnerungen und Health Connect bleiben für eine
  Web-App gesperrt. Das ist die größte Lücke zwischen Masterplan V8 und dem, was hier läuft,
  und sie ist nur über einen Capacitor-Wrapper zu schließen.
- Zweiwegesync mit Google Calendar: technisch machbar, braucht aber ein eigenes
  Google-Cloud-Projekt mit OAuth-Client und stündliche Token-Erneuerung.

## V5.7 — Zimmerplan und ein kritischer Speicherfehler (10.09.2026)

**KRITISCH, vor Auslieferung gefunden:** Die Sicherheitsrunde V5.6 hatte `const GIFT` unter
`let S = load()` gesetzt. `deepMerge` (hochgezogen) rief `GIFT` (temporale Totzone) → Fehler →
`load()` fiel stumm auf die Standardwerte → **jedes echte Neuladen löschte alle Eingaben.**
Nur in den noch nicht veröffentlichten V5.6-Dateien; die live genutzte V5.5 ist nicht betroffen.
Behoben (Reihenfolge korrigiert), Dauertest ergänzt. Lehre: Was `load()` beim Start braucht, muss
oberhalb stehen — hochgezogene Funktionen täuschen, ihre const-Abhängigkeiten sind es nicht.

**Zimmerplan** aus der Übergabe-Spezifikation vom 09.09.2026 gebaut: 35 Schritte, zehn Bereiche
A–J, fest sortiert, immer nur ein Schritt sichtbar, kurze Fassung zählt, Tief-Fenster und
Abendrunde zeitgesteuert, keine Serie. Als Nebeneinheit im Haushalt; der generische Haushalt
klappt ein, solange der Plan läuft, gegen Überfrachtung.

**Drei Alltagsfixes aus Eingang und Export:** Android-Zurück wirft nicht mehr aus der App
(eigener Verlauf); Essensfenster verankern sich an der tatsächlichen Einnahmezeit statt an 08:15;
Venenengel als ehrlich eingeordnete Regenerationskarte (kein belegter Nutzen, PubMed leer).

Tests 81 → 93, alle grün. Rückfallpunkt `/tmp/build/index.v56.bak`.

**Noch offen (unverändert):** Morgen-/Abendroutine in Unterschritte; Ernährungsausbau
(Wochenbudget, Allergien, Kochmöglichkeiten); drei Zeitangaben (Trainingsende Mo/Mi, Schlafenszeit,
Koffein). Aus dem Eingang neu und offen: Trainingsplan mit Regeneration + Gym + Spiel; zwei
Claude-Videokurse; „Gedanken parken" schließt noch die Tastatur.

## V5.6 — Prüfung durch das App Engineering Studio (10.09.2026)

Vier Prüfagenten über den Ist-Zustand von V5.5. Zwei Sperrvermerke:

- **Sicherheit und Datenschutz: BLOCK.** Nutzertext lief an acht Stellen als Code
  (`onclick` mit `esc()` — reicht nicht, siehe QUELLEN 13.1). Reproduziert, behoben,
  gegen die alte Fassung gegengeprüft. Dazu `deepMerge` gegen `__proto__` gesichert,
  Import auf bekannte Felder begrenzt, CSP eingezogen.
- **Recht: PRÜFUNG ANGERATEN.** Nicht wegen der App — wegen des öffentlichen Repos.
  Offen, Maiks Entscheidung.

Funktional dazu: Medikamentenwarnung erlosch ausgerechnet bei Bestand null. Bereitschaft war
rot eingefärbt und las sich wie ein Befund. Haushaltskachel zeigte die Rückstandszahl.
Zoom war gesperrt, Tap-Ziele unter 24 px, Hilfstexte unter 4,5:1 Kontrast.

Alles Behobene ist durch acht neue Dauertests abgedeckt — Testzahl 73 → 81, alle grün.
Rückfallpunkt `/tmp/build/index.v55.bak`.

**Bewusst offen gelassen, weil unumkehrbar oder Maiks Entscheidung:** Repo-Sichtbarkeit,
Entfernen persönlicher Passagen, Umschreiben der Git-Historie.

## Gelernt

Zwei Blöcke waren im Quelltext doppelt vorhanden — identisch, deshalb im Betrieb unauffällig,
aber ein indexbasierter Textersatz hat dadurch vier Funktionen mitgelöscht. Regel daraus:
Funktionen nur über Klammer-Matching ersetzen, nie über die Position der nächsten Funktion,
und nach jedem strukturellen Eingriff die Funktionsnamen zählen.

## Arbeitsweise

Vor jeder Auslieferung: Syntaxprüfung, Playwright-Durchlauf mit gemockter Open-Food-Facts-Antwort,
Screenshot bei 390×844 ansehen, CACHE hochzählen, QUELLEN.md nachziehen.
