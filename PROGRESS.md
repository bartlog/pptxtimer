# PROGRESS – Folienuhr (bartlog/pptxtimer)

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
