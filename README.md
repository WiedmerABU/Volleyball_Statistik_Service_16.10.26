# VBC Interlaken – Service-Statistik (Testversion 0.2)

GitHub-Pages-fähige Web-App. Hauptnavigation **Teams | Neues Spiel | Live-Game | Archiv** (links nach rechts); responsive für Smartphone und Laptop.

## Aktualisierung eines bestehenden GitHub-Repositories

1. ZIP auf dem Laptop entpacken. **Nicht** das ZIP selbst hochladen.
2. Repository `vbci-service-statistik` öffnen → **Add file → Upload files**.
3. Alle App-Dateien im Hauptverzeichnis hochladen, bestehende Dateien ersetzen und **Commit changes** bestätigen. Die im Paket mitgelieferte Spezifikation kann ebenfalls hochgeladen werden.
4. Unter **Settings → Pages**: Branch `main`, Ordner `/(root)`; die Veröffentlichung unter **Actions** prüfen.
5. Website auf dem Smartphone öffnen und im Browser **Zum Startbildschirm hinzufügen** wählen.

## Datensicherung vor jedem Update

In der bisherigen App unter **Team(s) → Daten sichern (JSON)** eine Sicherung exportieren. Den Browser-Speicher **nicht** löschen. Die App verwendet bewusst denselben lokalen Speicherschlüssel wie Version 0.1. Browser- und Gerätewechsel synchronisieren Daten nicht automatisch.

## Status und Einschränkungen

Diese ZIP enthält eine **lauffähige Testversion** und den überarbeiteten **Ziel-Masterprompt**. Nicht alle Spezifikationsanforderungen sind bereits programmiert. Insbesondere sind Spielerwechsel noch nicht vollständig auf Regelkonformität geprüft, der Matchentwurf wird nicht dauerhaft gespeichert, die Archivanalysen sind vereinfacht und die App nutzt `localStorage` statt der für spätere Ausbaustufen empfohlenen IndexedDB. Vor realen Wettbewerbsspielen fachlich testen.

## Dateien

`index.html`, `app.js`, `style.css`, `logo.png`, `icon.svg`, `manifest.webmanifest`, `README.md`, `MASTERPROMPT_GESAMT.md`.
