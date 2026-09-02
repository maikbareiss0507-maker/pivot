# Pivot — Trainings-, Last- und Ernährungstracker

Eine Progressive Web App. Läuft im Browser, installiert sich als Icon auf dem Homescreen,
funktioniert offline und speichert alles ausschließlich lokal auf dem Gerät.
Kein Konto, kein Server, keine Datenübertragung — die einzige externe Verbindung ist die
Produktabfrage bei Open Food Facts beim Scannen.

## Online stellen — Weg 1: Netlify Drop (schnellster Weg, ~2 Minuten)

1. Diesen Ordner als ZIP packen (oder das mitgelieferte `pivot-app.zip` nehmen).
2. https://app.netlify.com/drop öffnen und die ZIP-Datei ins Feld ziehen.
3. Du bekommst sofort eine HTTPS-Adresse wie `https://zufallsname.netlify.app`.
4. Kostenloses Netlify-Konto anlegen und die Seite dem Konto zuordnen — sonst ist sie
   nach einer Stunde wieder weg.
5. Unter *Site settings → Change site name* eine feste Adresse vergeben.

HTTPS ist zwingend: ohne HTTPS gibt der Browser keinen Kamerazugriff frei.

## Online stellen — Weg 2: GitHub Pages (dauerhaft, versioniert)

1. Auf github.com ein neues, öffentliches Repository anlegen, z. B. `pivot`.
2. *Add file → Upload files* — alle Dateien dieses Ordners hochladen, Commit.
3. *Settings → Pages → Source: Deploy from a branch → main / (root)* → Save.
4. Nach ein bis zwei Minuten liegt die App unter
   `https://<deinname>.github.io/pivot/`.

Willst du sie nicht öffentlich haben: Cloudflare Pages oder Vercel können dasselbe aus einem
privaten Repository heraus.

## Auf dem Handy installieren (Samsung Galaxy S23+)

1. Die Adresse in **Chrome** öffnen (nicht im Samsung Internet Browser — der unterstützt die
   BarcodeDetector-API nicht zuverlässig).
2. Menü ⋮ → **Zum Startbildschirm hinzufügen** → *Installieren*.
3. Beim ersten Scan-Versuch fragt Chrome nach der Kamera — erlauben.

Danach startet die App wie eine native App, ohne Adressleiste, und funktioniert auch ohne
Empfang. Nur der Barcode-Abgleich braucht Netz; unbekannte Produkte kannst du offline von
Hand eintragen und sie werden als Favorit gespeichert.

## Erste Schritte

1. **Profil** ausfüllen: Gewicht, Größe, Alter, Alltagsaktivität. Daraus entstehen alle Zielwerte.
2. **Tages-Check** jeden Morgen: vier Fragen, 20 Sekunden. Die App braucht vier Tage,
   bevor sie gegen deinen eigenen Schnitt statt gegen eine feste Skala rechnet.
3. **Einheiten** nach jedem Training erfassen — RPE etwa 30 Minuten nach Ende bewerten.
4. **Export** regelmäßig ziehen (Profil → Export). Löschst du die Browserdaten, sind alle
   Einträge weg.

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | Die komplette App — Oberfläche, Logik, Rechenmodelle |
| `manifest.webmanifest` | Macht die Seite installierbar |
| `sw.js` | Service Worker: Offline-Betrieb |
| `icon-*.png` | Homescreen-Icons |
| `QUELLEN.md` | Jede Rechenformel mit ihrer wissenschaftlichen Quelle |

## Was bewusst fehlt

- **Automatischer Import aus der Huawei Fit 3.** Huawei bietet keine offene Schnittstelle,
  und eine Web-App kommt grundsätzlich nicht an Android Health Connect. Schlaf und HRV
  müssen von Hand eingetragen werden. Erst ein nativer Wrapper (Capacitor + Health-Connect-Plugin)
  könnte das automatisieren.
- **Cloud-Sync zwischen Geräten.** Bewusst weggelassen — das würde einen Server und ein Konto
  bedeuten. Der JSON-Export erfüllt denselben Zweck manuell.
- **Ampelfarben für die Verletzungswahrscheinlichkeit.** Siehe `QUELLEN.md`, Abschnitt 4:
  die dafür übliche Kennzahl hält der Prüfung nicht stand.

## Aktualisieren, ohne Daten zu verlieren

Der Browserspeicher hängt an der **Adresse**, nicht an der Datei. Solange die Adresse gleich
bleibt, überlebt jede neue Version deine Einträge.

**So aktualisierst du richtig:**
1. Auf app.netlify.com einloggen und **deine bestehende Seite** öffnen.
2. Reiter **Deploys**.
3. Die neue ZIP in das Feld „Drag and drop your site output folder here" ziehen.
4. Fertig — gleiche Adresse, gleiche Daten.

**Nicht** erneut auf app.netlify.com/drop gehen. Das legt eine **neue** Seite mit **neuer**
Adresse an, und deine Einträge wären für die neue Adresse nicht sichtbar.

Auf dem Handy zeigt sich die neue Version beim übernächsten Öffnen — der Service Worker liefert
beim ersten Start noch die zwischengespeicherte Fassung und lädt die neue im Hintergrund.

## Später: Versionsverlauf über GitHub

Wenn du eine Historie deiner Änderungen willst, ist der richtige Weg **nicht** GitHub Pages,
sondern ein privates GitHub-Repository, das mit deiner bestehenden Netlify-Seite verbunden wird.
Netlify baut auch aus privaten Repositories. Damit bleibt die Adresse gleich, deine Daten bleiben
erhalten, und jede Änderung ist nachvollziehbar. GitHub Pages selbst verlangt auf dem
kostenlosen Plan ein öffentliches Repository.
