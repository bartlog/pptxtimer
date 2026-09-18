# Folienuhr – PowerPoint-Add-in

Setzt eine live laufende Anzeige direkt auf eine Folie. Sie läuft in der Bildschirmpräsentation weiter und lässt sich dort per Klick bedienen.

**Vier Modi**

- **Uhrzeit** – aktuelle Uhrzeit, sekundengenau, optional mit Datum
- **Countdown** – feste Dauer (z. B. 5:00), Warnfarbe kurz vor Ende, optional ins Minus weiterzählen, Signalton, Fortschrittsbalken, +1-Minute-Knopf
- **Bis Uhrzeit** – zählt bis zu einer Uhrzeit herunter („Weiter um 10:30“), läuft ohne Start
- **Stoppuhr** – zählt hoch

Pro Folie beliebig viele Instanzen, jede mit eigenen Einstellungen (werden in der .pptx gespeichert).

## Technik in einem Satz

Es ist ein **Inhalts-Add-in** (ContentApp): eine kleine Webseite, die PowerPoint als Objekt auf der Folie einbettet. Deshalb läuft JavaScript auch in der Präsentation – anders als bei Aufgabenbereich-Add-ins, die nur statische Inhalte in Folien schreiben können.

## 1. Hosten (einmalig)

Repository: https://github.com/bartlog/pptxtimer · Add-in-Adresse: `https://bartlog.github.io/pptxtimer/`

1. Im Repository „uploading an existing file“ wählen und den **Inhalt** dieses Ordners hineinziehen (`index.html`, `manifest.xml`, `README.md`, `PROGRESS.md` und den Ordner `assets`) – nicht den Ordner selbst, `index.html` muss direkt im Hauptverzeichnis liegen. Commit.
2. Settings → Pages → Source „Deploy from a branch“, Branch `main`, Ordner `/ (root)` → Save.
3. Nach ein, zwei Minuten prüfen: `https://bartlog.github.io/pptxtimer/` zeigt die Uhr, `https://bartlog.github.io/pptxtimer/assets/icon-80.png` das Icon.

**Updates:** Geänderte `index.html` einfach neu hochladen. Das Manifest musst du nur neu laden, wenn sich `manifest.xml` ändert. Zeigt PowerPoint noch die alte Version, PowerPoint neu starten; hilft das nicht, den Office-Cache leeren (Windows: `%LOCALAPPDATA%\Microsoft\Office\16.0\Wef\`, Mac: `~/Library/Containers/com.microsoft.Powerpoint/Data/Library/Caches/`).

**Woran du erkennst, ob eine Änderung angekommen ist:** Im Einstellungspanel steht oben immer die aktuelle Versionsnummer, z. B. „Folienuhr v1.2.0". Öffne dazu in PowerPoint das Zahnrad – steht dort die neue Nummer, läuft die neue `index.html`. Ein „yesterday" bei `manifest.xml` auf GitHub ist dabei normal und kein Fehlersignal: Diese Datei ändert sich nur, wenn sich Name, Icons oder Adresse ändern, nicht bei jedem Update der Anzeige selbst. GitHub setzt das Datum ohnehin nur, wenn sich der Dateiinhalt tatsächlich unterscheidet – ein erneuter Upload derselben Datei hinterlässt keinen neuen Commit.

## 2. In PowerPoint laden (Sideloading)

Die Menünamen unterscheiden sich je nach PowerPoint-Version leicht.

**PowerPoint im Web** (schnellster Test)
Einfügen → Add-Ins → Meine Add-Ins → *Mein Add-In hochladen* → `manifest.xml` wählen.

**PowerPoint für Mac**
1. Ordner anlegen (falls nicht vorhanden): `~/Library/Containers/com.microsoft.Powerpoint/Data/Documents/wef`
2. `manifest.xml` dort hineinkopieren.
3. PowerPoint neu starten → Einfügen → Add-Ins → Meine Add-Ins → Folienuhr.

**PowerPoint für Windows**
1. Einen Ordner mit `manifest.xml` im Netzwerk freigeben (auch lokal: Rechtsklick → Eigenschaften → Freigabe), Pfad z. B. `\\MEINPC\addins`.
2. Datei → Optionen → Trust Center → Einstellungen für das Trust Center → Vertrauenswürdige Add-In-Kataloge.
3. Den Freigabepfad als Katalog-URL eintragen, „Katalog hinzufügen“, Häkchen bei „Im Menü anzeigen“, OK.
4. PowerPoint neu starten → Einfügen → Add-Ins → Meine Add-Ins → Freigegebener Ordner → Folienuhr.

## 2b. Für die ganze Organisation freigeben (Microsoft 365 Admin Center)

Statt jedes Gerät einzeln einzurichten, lässt sich das Add-in einmal zentral bereitstellen. Es erscheint dann automatisch in PowerPoint auf allen Geräten der Nutzer, unter Windows, Mac und im Web, ohne lokale Manifest-Datei. Voraussetzung: ein Microsoft-365-Konto mit Admin-Rechten für den Mandanten.

1. Im [Microsoft 365 Admin Center](https://admin.microsoft.com) links auf **Einstellungen → Integrierte Apps**.
2. Unterhalb der vorgeschlagenen Apps auf **Benutzerdefinierte Apps hochladen** klicken (nicht die vorgeschlagenen Kacheln – die sind fremde Anbieter).
3. App-Typ **Office-Add-In** wählen, dann **Link zur Manifestdatei angeben** und eintragen:
   ```
   https://bartlog.github.io/pptxtimer/manifest.xml
   ```
   Auf **Überprüfen** klicken – das Manifest wird direkt von GitHub Pages geladen und validiert.
4. Bei **Benutzer** entweder „Nur ich“ oder bestimmte Personen/Gruppen wählen, je nachdem, wer Zugriff haben soll.
5. Berechtigungen bestätigen und auf **Bereitstellen** klicken.

Bis das Add-in in PowerPoint auftaucht, vergehen meist ein paar Stunden, im Extremfall bis zu 24. Es steht danach unter **Start → Add-Ins → Weitere Add-Ins → Vom Administrator verwaltet**.

**Updates laufen automatisch mit.** Da das Manifest nur auf die GitHub-Pages-Adresse verweist, reicht es, `index.html` im Repository zu aktualisieren – die zentrale Bereitstellung im Admin Center muss dafür nicht angefasst werden. Nur wenn sich `manifest.xml` selbst ändert (Name, Icons, Adresse), muss der Upload im Admin Center wiederholt werden.

**Aufräumen:** Wurde das Add-in vorher lokal oder über einen freigegebenen Ordner eingebunden (siehe Trust-Center-Weg oben), taucht es sonst doppelt auf. Die lokale Kopie bzw. den freigegebenen Ordner dann entfernen.

## 3. Benutzen

1. Add-in einfügen – beim ersten Mal öffnen sich die Einstellungen automatisch.
2. Modus, Dauer, Beschriftung, Farben und Schrift wählen → **Fertig**. Später über das Zahnrad oben rechts ändern.
3. Objekt auf der Folie wie ein Bild verschieben und skalieren. Die Ziffern passen sich der Größe an.
4. In der Bildschirmpräsentation:
   - Klick auf die Anzeige: Start / Pause
   - Doppelklick: zurücksetzen
   - Maus bewegen: Knöpfe für Start/Pause, Zurücksetzen und +1 Minute erscheinen

**Schriften:** Systemschrift, Roboto Condensed, Roboto Mono, Roboto Slab, Roboto, Literata, Outfit – jeweils Light, Normal, Medium oder Bold, auf Wunsch kursiv. Roboto Slab und Outfit haben keine echte Kursive; dort wird schräg gestellt. Alle Ziffern stehen auf fester Breite, damit die Anzeige beim Zählen nicht wackelt.

**Farben:** Vier fertige Schemata oder „Eigene“ mit freier Hex-Eingabe (`#236292` o. ä.) für Schrift, Hintergrund, Balken und Warnung – per Farbwähler, Text oder Pipette direkt von der Folie (siehe unten).

## Lokal ausprobieren

`index.html` einfach im Browser öffnen. Einstellungen über das Zahnrad, „Präsentationsansicht testen“ simuliert die Präsentation (Esc kehrt zurück).

## Gut zu wissen

- **Internet nötig.** PowerPoint lädt die Seite von GitHub Pages und `office.js` von Microsoft. Vor einem Workshop an fremden Orten kurz testen.
- **Autostart** erkennt die Folie, auf der das Add-in liegt, und startet, sobald sie in der Präsentation erscheint. Das hängt davon ab, dass PowerPoint die aktuelle Folie meldet – einmal vorher testen. Klappt es nicht, startet der Timer beim Beginn der Präsentation bzw. per Klick. Wurde die Folie dupliziert, einmal das Zahnrad öffnen, damit sich die neue Folie gemerkt wird.
- **Folie verlassen und zurückkehren**: Ein laufender Countdown läuft weiter. Nach Ende der Präsentation wird zurückgesetzt.
- **Signalton**: Browser erlauben Ton oft erst nach einer Interaktion. Bei Autostart ohne Klick kann der Ton stumm bleiben; ein Klick auf die Anzeige (Start) schaltet ihn frei.
- **Tastatur**: Nach einem Klick in die Anzeige hat das Add-in den Fokus. Pfeiltasten/Leertaste gehen dann an das Add-in statt an die Präsentation – einmal neben die Anzeige auf die Folie klicken oder den Presenter nutzen.
- **Kein durchsichtiger Hintergrund.** PowerPoint stellt Add-in-Inhalte immer auf einem eigenen, deckenden Untergrund dar, technisch ist das nicht zu umgehen. Passe stattdessen die Hintergrundfarbe unter „Eigene“ exakt an die Folie an. Am schnellsten geht das mit der Pipette neben dem Farbfeld: Klick darauf und wähle direkt eine leere Stelle der Folie. Die Pipette gibt es aktuell nur in Chromium-Browsern (PowerPoint unter Windows und im Web); erscheint sie nicht, z. B. am Mac, liest du die Farbe stattdessen über **Entwurf → Hintergrund formatieren → Weitere Farben** ab und trägst sie von Hand ein. Bei Verlaufs- oder Bildhintergründen gibt es ohnehin keine einzelne passende Farbe.
- **Weitergabe der Datei**: Wer das Add-in nicht installiert hat, sieht statt der Live-Anzeige ein Standbild (Snapshot). Zum Präsentieren auf einem anderen Rechner das Add-in dort ebenfalls laden.

## Dateien

```
pptxtimer/
├── index.html      Anzeige, Timer-Logik, Einstellungen (eine Datei, kein Build)
├── PROGRESS.md     Stand und offene Prüfpunkte
├── manifest.xml    Add-in-Beschreibung für PowerPoint
└── assets/         Icons 16/32/64/80 px
```
