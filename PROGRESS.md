# PROGRESS – Folienuhr (bartlog/pptxtimer)

## Stand v1.2 (Manifest-Version 1.2.0.0)
- Sichtbare Versionsnummer im Einstellungspanel (Konstante APP_VERSION in index.html), zur Kontrolle nach jedem Update ohne Umweg über GitHub-Zeitstempel
- Konvention ab jetzt: bei inhaltlichen Änderungen an index.html sowohl APP_VERSION als auch <Version> in manifest.xml gemeinsam anheben
- Farben "Eigene": Hex-Textfelder neben den Farbwählern (Schrift/Hintergrund/Balken/Warnung), bidirektional synchron, ungültige Eingabe wird optisch markiert und nicht übernommen
- Deckkraft-Regler 0–100 % (10er-Schritte) für das gesamte Element (opacity auf documentElement), unabhängig von der Hintergrund-Transparenz
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
