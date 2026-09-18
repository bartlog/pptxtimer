# PROGRESS – Folienuhr (bartlog/pptxtimer)

## Stand v1.3 (Manifest-Version 1.3.0.0)
- **Erkenntnis aus echtem PowerPoint-Test:** Inhalts-Add-ins rendern immer auf einem eigenen, deckenden Untergrund; CSS-Transparenz und Element-Opacity werden vom Host ignoriert bzw. blenden nur zu Grau. Beides in v1.2 eingeführt, in v1.3 wieder entfernt: Checkbox "Hintergrund transparent" und Regler "Deckkraft gesamt" (samt CSS `.transparent`, `documentElement.style.opacity`, State-Felder `transparent`/`opacity`)
- Stattdessen: Pipetten-Button neben jedem Hex-Feld (Schrift/Hintergrund/Balken/Warnung) über die `EyeDropper`-API, zum direkten Farbabgleich mit der Folie. Feature-Detection via `"EyeDropper" in window`; ohne Unterstützung (Safari/Mac) wird der Button per `body.no-eyedropper` ausgeblendet, Hex-Textfeld bleibt nutzbar
- Neuer Hinweistext im Panel erklärt die Grenze offen und verweist auf den Farbabgleich als Workaround
- README: Abschnitt "Gut zu wissen" entsprechend korrigiert (vorher fälschlich "nicht in jeder Version unterstützt" – tatsächlich in keiner aktuellen Version)

## Stand v1.2 (Manifest-Version 1.2.0.0)
- Sichtbare Versionsnummer im Einstellungspanel (Konstante APP_VERSION in index.html), zur Kontrolle nach jedem Update ohne Umweg über GitHub-Zeitstempel
- Konvention ab jetzt: bei inhaltlichen Änderungen an index.html sowohl APP_VERSION als auch <Version> in manifest.xml gemeinsam anheben
- Farben "Eigene": Hex-Textfelder neben den Farbwählern (Schrift/Hintergrund/Balken/Warnung), bidirektional synchron, ungültige Eingabe wird optisch markiert und nicht übernommen
- ~~Deckkraft-Regler 0–100 % (10er-Schritte) für das gesamte Element~~ – siehe v1.3, wieder entfernt
- README: Abschnitt 2b zur zentralen Bereitstellung über Microsoft 365 Admin Center → Integrierte Apps, mit Verweis auf die GitHub-Pages-Manifest-URL

## Stand v1.1
- Hosting: https://bartlog.github.io/pptxtimer/ (Repo bartlog/pptxtimer)
- Schriften: Systemschrift, Roboto Condensed, Roboto Mono, Roboto Slab, Roboto, Literata, Outfit (Google Fonts); Stärke 300/400/500/700; Kursiv (Slab/Outfit synthetisch)
- Ziffern mit fester Breite (breiteste Ziffer je Schrift gemessen), alte Schrift-Einstellungen werden migriert

## v1.0.0
- Inhalts-Add-in (ContentApp) für PowerPoint, eine index.html ohne Build
- Modi: Uhrzeit, Countdown, Bis Uhrzeit, Stoppuhr
- Einstellungen pro Instanz über Office.context.document.settings (Browser-Vorschau: localStorage)
- Ansichtserkennung edit/read über getActiveViewAsync + ActiveViewChanged
- Autostart per Folien-ID-Abgleich (getSelectedDataAsync SlideRange, Polling 400 ms) mit Fallback
- Im Browser getestet (Chromium): Anzeige, Einstellungen, Countdown, Ablauf, Bedienknöpfe

## Noch in echtem PowerPoint zu prüfen
- Windows, Mac, Web: Live-Aktualisierung in der Bildschirmpräsentation
- Autostart-Erkennung der aktuellen Folie in der Präsentation
- Transparenter Hintergrund
- Signalton ohne vorherigen Klick
- Google Fonts laden im PowerPoint-Webview (sonst Fallback-Schrift)
