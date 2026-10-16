# VBC Interlaken – Service Statistik (Testversion 0.3)

Responsive Web-App für Volleyball-Serviceerfassung. Installation über GitHub Pages.

## Installation im vorhandenen GitHub-Repository

1. Vor dem Update bestehende Daten in **Teams → Daten sichern (JSON)** exportieren, falls möglich.
2. ZIP entpacken; **die einzelnen Dateien** in das Root-Verzeichnis des bestehenden GitHub-Repositories hochladen (nicht die ZIP selbst).
3. Änderungen auf `main` committen. In GitHub `Settings → Pages → Deploy from a branch → main → /(root)` wählen (falls noch nicht aktiv).
4. Deployment unter `Actions` kontrollieren; anschliessend die bereits bekannte GitHub-Pages-Adresse öffnen.
5. Wenn die alte Ansicht erscheint, Browserseite hart aktualisieren. Auf Samsung über Chrome/Edge zum Startbildschirm hinzufügen.

## Neu in Version 0.3

- Aufstellung mit perspektivischer Volleyball-Feldgrafik, aus Sicht **hinter der eigenen Grundlinie**, in der Spielvorbereitung und im Live-Game.
- VBCI-orientierte blaue Oberfläche, responsive verfeinert.
- Bei `Neues Spiel` entfällt `Spielort`; erster Service wird erst bei `Aufstellung` gewählt.
- Teamwahl im Screen `Neues Spiel` und automatische Vorauswahl der aktiven Teamspieler/-innen.
- Grundlegende Zurück/Vorwärts-Funktion während eines laufenden Satzes.

## Bekannte Einschränkungen (wichtig)

- **Testversion, nicht vollständig regelgeprüft.** Spielerwechsel und Rückwechsel sind noch nicht vollständig wettbewerbsregelkonform umgesetzt.
- Die Verlaufsnavigation ist aktuell **satzbezogen**, nicht umfassend über Satzwechsel/Archivierung hinweg. Die im Masterprompt definierte vollständige Historie bleibt Entwicklungsziel.
- Satz-5-Sonderregeln wie Seitenwechsel beim 8. Punkt sind noch nicht umfassend implementiert.
- Die neue Feldgrafik ist eine **schematische 3D-artige Perspektive** (CSS), keine reale 3D-Spielsimulation.
- Datenspeicherung ist lokal im Browser, **keine Geräte-Synchronisierung**. Browserspeicher nicht löschen; JSON-Backup anlegen.
- Nicht alle im `MASTERPROMPT_GESAMT.md` beschriebenen Archiv- und UX-Funktionen sind schon eingebaut.

## Dateien

`index.html`, `app.js`, `style.css`, `logo.png`, `icon.svg`, `manifest.webmanifest`, `MASTERPROMPT_GESAMT.md`, `README.md`.
