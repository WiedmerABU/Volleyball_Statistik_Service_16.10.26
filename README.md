VBCI Service Statistik App – Update v0.5

Enthält die vergrösserte blaue Feldgrafik, damit die Karten von Position 1, 2, 4 und 5 vollständig innerhalb des Feldes sichtbar sind.

# VBC Interlaken – Service Statistik (Testversion 0.4)

Responsive Web-App für Volleyball-Serviceerfassung. Installation über GitHub Pages.

## Installation im vorhandenen GitHub-Repository

1. Vor dem Update bestehende Daten in **Teams → Daten sichern (JSON)** exportieren.
2. ZIP entpacken; **die einzelnen Dateien** in das Root-Verzeichnis des bestehenden GitHub-Repositories hochladen (nicht die ZIP selbst).
3. Änderungen auf `main` committen. GitHub Pages bleibt unter `Settings → Pages → Deploy from a branch → main → /(root)` aktiviert.
4. Veröffentlichung unter `Actions` kontrollieren; dann die bestehende GitHub-Pages-Adresse öffnen.
5. Bei alter Ansicht Seite neu laden bzw. auf Samsung Cache aktualisieren.

## Neu in Version 0.4

- **Fehler beim Erstellen von Satz 2 behoben:** Die Auswahl der sechs neuen Startspielerinnen wird bei jedem Eingabeschritt beibehalten.
- **Satz 2, 3, 4 und ggf. 5:** Die sechs Aufstellungspositionen können nun direkt in der schematisch perspektivischen Feldgrafik mit Spielerinnen aus dem Matchkader besetzt werden.
- Zu jeder Trikotnummer erscheinen Name und optionales Positionskürzel. Doppelte, fehlende oder unzulässige Auswahlen blockieren die Bestätigung.
- Die Auswahl bleibt für jeden Satz unabhängig; frühere Satzstatistiken bleiben erhalten.
- Die aktuelle Feldgrafik ist auch im Live-Game abrufbar.

## Bekannte Einschränkungen

- Testversion, **nicht vollständig regelgeprüft**. Spielerwechsel und Rückwechsel sind noch nicht wettbewerbsregelkonform vollständig implementiert.
- Undo/Redo ist derzeit satzbezogen; satzübergreifende Historie ist noch nicht implementiert.
- Entscheidungssatz: Der Seitenwechsel bei 8 Punkten wird noch nicht vollständig verwaltet.
- Lokale Speicherung im Browser (localStorage), keine Synchronisation zwischen Geräten. JSON-Backups anlegen und Browserdaten nicht löschen.
- Funktionen aus dem Gesamt-Masterprompt, beispielsweise erweiterte Archivstatistiken und neue Team-Dialoge, sind noch nicht vollständig umgesetzt.

## Dateien

`index.html`, `app.js`, `style.css`, `logo.png`, `icon.svg`, `manifest.webmanifest`, `MASTERPROMPT_GESAMT.md`, `README.md`.
