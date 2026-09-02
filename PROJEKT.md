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

## Gelernt

Zwei Blöcke waren im Quelltext doppelt vorhanden — identisch, deshalb im Betrieb unauffällig,
aber ein indexbasierter Textersatz hat dadurch vier Funktionen mitgelöscht. Regel daraus:
Funktionen nur über Klammer-Matching ersetzen, nie über die Position der nächsten Funktion,
und nach jedem strukturellen Eingriff die Funktionsnamen zählen.

## Arbeitsweise

Vor jeder Auslieferung: Syntaxprüfung, Playwright-Durchlauf mit gemockter Open-Food-Facts-Antwort,
Screenshot bei 390×844 ansehen, CACHE hochzählen, QUELLEN.md nachziehen.
