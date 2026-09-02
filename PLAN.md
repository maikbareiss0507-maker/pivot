# Pivot — Ausbauplan

Stand 02.09.2026. Festgelegt nach Maiks Rückmeldung zum Umfang.

## Leitsatz

Pivot besitzt die **Ausführung seines Tages** — was er tut, isst, trainiert, wie er sich fühlt,
und was ihm dabei hilft anzufangen. Wissen bleibt in Obsidian. Alles andere zieht nur ein,
wenn Pivot es *besser* macht als das bestehende Werkzeug, nicht bloß zusätzlich.

Der Prüfstein bei jeder neuen Funktion: **Bricht sie die Zehn-Sekunden-Regel?** Wenn eine
Eingabe länger dauert, wird sie ausgelassen, und die Lücke entwertet die ganze Erfassung.

## Aufgenommen

| Baustein | Was es tut |
|---|---|
| **Zigaretten** | Zähler mit einem Tap plus Auslöserfrage: Situation, Ort, Gefühl. Tagessumme und Wochenverlauf. Die häufigsten Auslöser werden automatisch zu Vorschlägen für Wenn-dann-Regeln. |
| **Nullschritt-Drills** | Tägliche Mini-Einheiten mit Zähler, drei bis sieben am Tag à etwa 20 Wiederholungen. Auch kleinere Einheiten zählen. Gibt der App an trainingsfreien Tagen einen Zweck. |
| **Wochenblick** | Trainingswoche, Essensfenster-Quote, Befinden, Zigaretten, offene Anker. Sonntagabend, mit kurzer Erinnerung — bewusst auf wenige Minuten begrenzt, kein Wochenritual mit Eskalationsgefahr. |
| **Wochenanker Beziehung** | Eine feste Sache mit Evi pro Woche, jederzeit sichtbar und abhakbar. |
| **Journaling und Tagesreflexion** | Kommt herein. Begründung siehe unten. Kurzform: drei Fragen abends, freies Textfeld, Rückblick über die Woche. |
| **ADHS-Werkzeugkasten** | Situationskarten: „Ich komme nicht in Gang", „Ich bin überdreht", „Ich habe drei Sachen offen und mache keine", „Ich verliere im Spiel den Faden". Je zwei bis drei konkrete Handgriffe. Keine Symptomskalen, keine Diagnostik, keine Medikationshinweise. |
| **Impulskauf-Check** | Kurzer Fragenlauf vor einem Kauf, mit 24-Stunden-Regel und Wiedervorlage. Nicht abschreckend gemeint, sondern entscheidungsentlastend. |
| **Evidenz im Hintergrund** | Das bestehende „Warum?" wird auf alle neuen Bausteine ausgeweitet: Bedeutung, Quelle, Grenze. Ziel ist, dass Maik nichts nachgoogeln muss. |
| **Bericht für Claude** | Ein Knopf erzeugt eine kompakte Zusammenfassung der letzten Tage, die Maik in einem Tap in den Chat teilen kann. Damit sieht Claude die echten Daten, ohne dass ein Server nötig wird. |

## Zurückgestellt, mit Begründung

**Studium** — kommt erst, wenn Blöcke und Zeiten des DHGS-Studiums feststehen. Vorher wäre es
geraten.

**Kalender in Pivot** — in zwei Stufen. Stufe eins ist ein eigener Kalender in Pivot, der lokal
läuft: schnelles Eintragen in zwei Taps, an Maiks Tagesphasen und Anker angepasst, mit
Funktionen, die Google Calendar nicht hat. Stufe zwei ist die Verbindung zu Google Calendar über
OAuth. Das ist aus einer reinen Web-App machbar, verlangt aber ein eigenes Google-Cloud-Projekt
mit OAuth-Client, und die Zugangstoken laufen stündlich ab und müssen im Hintergrund erneuert
werden. Erst Stufe eins bauen und prüfen, ob Pivot als Eingabeort überhaupt gewinnt — sonst
entstehen zwei Kalender mit demselben Inhalt, also genau das, was vermieden werden soll.

**Automatischer Schlafimport** — nicht möglich. Siehe unten.

## Nicht machbar, und warum

**Schlafdaten aus Samsung Health oder Health Connect auslesen.** Health Connect ist eine
Android-Schnittstelle für native Android-Apps. Eine Web-App im Browser hat darauf grundsätzlich
keinen Zugriff, unabhängig von Berechtigungen. Das gilt genauso für Samsung Health und Huawei
Health.

Was stattdessen geht:
1. **Schlafdauer und Schlafqualität von Hand** in den Tages-Check eintragen — der Wert ist
   ohnehin schon da, es sind zwei Eingaben.
2. **Analyse und Hinweise** baut die App auf diesen Daten auf: Regelmäßigkeit der Bettzeit,
   Dauer, Zusammenhang mit Trainingslast und Befinden. Dafür braucht es keine Uhr.
3. **Langfristig**: die App per Capacitor in eine native Android-Hülle packen. Dann darf sie
   Health Connect lesen. Das ist ein eigenes Projekt mit Android Studio und Signaturschlüssel.

## Bewusst weiterhin draußen

- Notizen und Wissensdatenbank — bleibt Obsidian
- ADHS-Diagnostik, Symptomskalen, alles was nach Behandlung aussieht — bleibt bei Psychiaterin
  und Attexis
- Detailliertes Finanztracking — der Impulskauf-Check ist eine Entscheidungshilfe, keine
  Buchhaltung
- Gamification, Punkte, Ränge, Streaks — aus demselben Grund wie bisher

## Warum Journaling doch hereinkommt

Ursprünglich hatte ich abgeraten, um keine Dopplung zu Liven zu schaffen. Maiks Einwand hat das
widerlegt: Liven kostet Geld und wird kaum geöffnet, selbst mit Kalendereintrag. Eine schlechtere
Funktion in einer App, die er täglich sowieso benutzt, schlägt eine bessere in einer App, die er
nicht öffnet. Das ist dasselbe Prinzip, auf dem die ganze ADHS-Schicht steht.

Folge daraus: Sobald das Journaling in Pivot läuft und zwei Wochen benutzt wurde, gehört das
Liven-Abo gekündigt. Zwei Orte für dieselbe Sache heißt, dass keiner benutzt wird.

## Baureihenfolge

1. Zigaretten, Nullschritt-Drills, Wochenanker Beziehung — klein, sofort nutzbar, kein Risiko
2. Journaling und Tagesreflexion, ADHS-Werkzeugkasten
3. Wochenblick und Impulskauf-Check
4. Bericht für Claude
5. Kalender Stufe eins
6. Schlafanalyse auf den vorhandenen Daten

Vorher: Umzug auf GitHub Pages, weil Netlify auf dem kostenlosen Plan nur etwa zwanzig
Veröffentlichungen im Monat erlaubt und die Seite danach pausiert.
