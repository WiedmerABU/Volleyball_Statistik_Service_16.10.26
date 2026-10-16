# VBC INTERLAKEN – GESAMT-MASTERPROMPT VOLLEYBALL-SERVICE-STATISTIK

**Spezifikation 2.0 · 16.10.2026 · GitHub Pages / responsive Web-App**

## 0. Entwicklungsauftrag und verbindliche Prioritäten

Entwickle eine moderne, robuste, intuitiv bedienbare Volleyball-Service-Statistik-Web-App für Desktop, Tablet und Smartphone auf Basis des unveränderten VBC-Interlaken-Logos. Die Hauptaufgabe ist die schnelle und zuverlässige Erfassung eigener Aufschläge und des dazugehörigen Ballwechselverlaufs während eines Matches. Die App muss ohne Backend über GitHub Pages lauffähig sein. Alle vier Hauptscreens teilen ein konsistentes Datenmodell. Regeln für Sonderwettbewerbe müssen explizit konfigurierbar bleiben; nichts unbemerkt erfinden.

**Navigation exakt von links nach rechts:** **Teams | Neues Spiel | Live-Game | Archiv**. Auf Smartphone permanente Bottom Navigation mit Safe-Area-Abstand, auf Laptop adaptiv. Aktiven Screen hervorheben. Eigenes Team in allen Score- und Matchansichten links, Gegner rechts.

**Qualität:** Primär Smartphone-Hochformat; grosse Touchflächen mindestens 44×44 px; optimale Kontraste, klare Zustandsanzeigen und bedienbare Buttons. Wichtiges wird durch **ruhiges, langsames Pulsieren** hervorgehoben, nie mehrere konkurrierende Animationen. `prefers-reduced-motion` respektieren. Keine Informationsüberladung. Alles mit wenigen Aktionen. Speichern nach jeder abgeschlossenen Änderung; Fehlbedienungen müssen konsistent korrigierbar sein. Farben exakt aus dem bereitgestellten Logo ableiten und als Design-Tokens zentral pflegen; nie das Logo verändern.

## 1. Screen TEAMS – Stammdaten

### 1.1 Vorhandene und neue Teams trennen

- Zwei klar sichtbare Einstiegspunkte: **Vorhandene Teams** und **Neues Team erstellen**.
- Vorhandene Teams geordnet nach Verein und Saison anzeigen. Teamkarte nennt die vollständige Bezeichnung, etwa `VBC Interlaken – Damen 4. Liga – Gruppe A`, Saison und Anzahl aktiver Spielerinnen.
- Team öffnen führt zum **dauerhaft gespeicherten Teamkader**; zwischen Vereinen/Teams schnell wechseln.
- Neues Team: Verein als Pflichtfeld erfassen oder vorhandenen Verein auswählen; Saison erfassen oder auswählen (`2026/27`); Kategorie/Liga/Gruppe wählen; automatisch generierte Mannschaftsbezeichnung und eindeutige Team-ID speichern.

### 1.2 Kategorien und dynamische Auswahl

| Kategorie | Liga / Alter | Gruppe |
|---|---|---|
| Damen | 1.–5. Liga | Optional A/B/C/D nur 3.–5. Liga |
| Herren | 1.–4. Liga | Optional A/B/C/D nur 3.–4. Liga |
| Mixed | Keine | Keine |
| Juniorinnen | U14 / U16 / U18 / U20 / U23 | Keine |
| Junioren | U14 / U16 / U18 / U20 / U23 | Keine |

Nicht relevante Felder ausblenden, ungültige Altwerte beim Wechsel zurücksetzen. Mehrere Teams und Saisons unabhängig verwalten.

### 1.3 Teamkader

- Pro Person Pflicht: Trikotnummer **0–99**, Vorname, Nachname. Freiwillige Standardrolle: `P` Passeuse / `A` Aussen / `M` Mitte / `D` Diagonal / `L` Libera/Libero / keine Angabe.
- UI-Eingabe: schmaler Nummernblock, Vorname daneben, Nachname darunter, Position als antippbare Buchstaben. Kader nach Nummer sortiert; aktive Nummern eindeutig.
- Personen hinzufügen, bearbeiten, deaktivieren/reaktivieren, Nummer/Rolle verändern; gesamten Kader in neue Saison kopieren und dann anpassen. Dauerhafte IDs.
- **Historische Unveränderlichkeit:** Bei Änderung einer Trikotnummer werden nur künftige Matchkader aktualisiert. Schon eröffnete, laufende und archivierte Spiele zeigen weiterhin ihre ursprünglich gespeicherte Nummer, Namen und Rollen. Die Spieler-ID bleibt stabil und Match-Snapshots erhalten historische Daten.
- Lokale Datensicherung JSON exportieren/importieren inkl. Versionsschema und Validierung. Keine automatische geräteübergreifende Synchronisierung behaupten.

## 2. Screen NEUES SPIEL – drei Schritte

### 2.1 Spieldaten

- Links aus **vorhandenen Teams** wählen, rechts Gegnername (Pflichtfeld) eingeben; Datum (Pflichtfeld). **Kein Spielort.**
- **Hier noch KEINE Auswahl des ersten Service.**
- Vorhandene laufende Spiele getrennt anzeigen: fortsetzen oder als «Nicht abgeschlossen» ins Archiv verschieben.

### 2.2 Matchkader

- Nach Teamwahl werden **alle aktiven Personen automatisch vorausgewählt**. Nicht teilnehmende Personen mit einem Tipp abwählen. Bis zwei zusätzliche Gastspieler/-innen für das konkrete Match aufnehmen. Keine Veränderung am dauerhaften TEAM-Kader durch Änderungen im Matchkader.
- Zu jedem Match werden historische Stammdaten kopiert. Rollen P/A/M/D/L können für das Match angepasst werden. Matchkader ist getrennt vom Teamkader gespeichert.

### 2.3 Startaufstellung und erster Service

- Für **jeden Satz 1–5** werden die sechs Startspieler/-innen **neu aus dem Matchkader** gewählt; **nicht** aus dem vorherigen Satz. Ab Satz 2 reichen die sechs Trikotnummern; Namen und zuletzt für das Match gewählte Positionskürzel ergänzen sich automatisch.
- Sechs unterschiedliche, matchberechtigte Feldspieler/-innen prüfen, und **erst nach Bestätigung** die Satzaufstellung speichern.
- **Aufstellungszettel, Blick aus eigenem Hinterfeld:** Netz oben, vorn `4 3 2`, hinten `5 6 1`. Alle sechs Feldkarten zeigen Nummer, Name und gegebenenfalls Rollen-Kürzel.
- Die Libera ist **separat in Spalte 1, Zeile 3** als Anzeige mit Nummer, Name und `L`; keine siebte Rotationsposition und keine eigenständige Libera-Einsatzverwaltung. Die Libera darf in dieser Service-App nicht als servierende Person erscheinen.
- Neben dem schematischen Positionszettel eine **grafische Feldansicht in Tiefenperspektive** anbieten, aus Sicht **hinter der Grundlinie des eigenen Teams**. Perspektive muss klar lesbar bleiben. Grundlinie unten nahe Betrachter, Netz oben weiter entfernt; hinten `5 6 1`, vorne `4 3 2`.
- **Erst hier**, im Schritt **Aufstellung Satz 1**, wählen: `1. Service eigenes Team` oder `1. Service Gegner`. Auswahl exklusiv, kein Default, speichern und an Live-Game übergeben.
- Grosser Button **«Spiel eröffnen» über die volle Inhaltsbreite**. Keine doppelten Matches durch Doppeltippen; unvollständige Vorbereitung nicht starten.

## 3. Screen LIVE-GAME – Echtzeitservice

### 3.1 Grundansicht

- Punkte und Teams immer nebeneinander: eigenes Team **links**, Gegner **rechts**. Grosse Zahlen. Alle aktiven Aktionen fingerfreundlich, keine ungewollten Doppelbuchungen.
- Dynamischer Bildschirm: Bei eigenem Aufschlag grosse Karte mit **Trikotnummer, vollständigem Namen, optionalem P/A/M/D-Kürzel**, aktueller Rotationsposition 1; blauer pulsierender Rahmen. Drei grosse Schaltflächen `ASS | NORMAL | FEHLER`.
- Bei gegnerischem Service wird Gegnerbereich **rot pulsierend** angezeigt. Zwei getrennte Punktebuttons **direkt unter den jeweiligen Teamspalten**, links `+ Punkt eigenes Team`, rechts `+ Punkt Gegner`, **nicht über gesamte Breite**.
- Globale Browsernavigation bleibt erreichbar; kein ungespeicherter Statusverlust.

### 3.2 Serviceereignisse / Spielverlauf

- `ASS`: eigener Punkt +1; Ass für aktuelle Aufschlagperson verbuchen; gleiche Person bleibt am Service.
- `FEHLER`: Gegner +1; Servicefehler der Spielerin zuordnen; Wechsel zur Gegner-Serviceansicht, **keine Rotation** des eigenen Teams.
- `NORMAL`: zunächst laufenden Ballwechsel markieren; anschließend genau einer von zwei Buttons `Punkt eigenes Team` / `Punkt Gegner`. Erst nach Ergebnis **eine** abgeschlossene Normal-Serviceaktion speichern. Eigener Punkt => gleiche Person serviert weiter; Gegnerpunkt => gegnerische Serviceansicht.
- Bei gegnerischem Aufschlag: Gegnerpunkt => Gegner bleibt am Service, eigenes Team +1 nach gewonnenem Ballwechsel => **Side-out mit genau einer Rotation** und unmittelbarer Wechsel zur **neuen Aufschlagperson auf Position 1**.
- Rotation des eigenen Teams **nur** nach Gewinn des Aufschlagrechts: `2→1→6→5→4→3→2`. Nie beim Aufschlagverlust. Aus offiziell gespeicherter Startaufstellung berechnen, nicht aus Anzeigenamen.
- Jeder eigene Service der statistischen **Punktestandphase vor Aufschlag** zuordnen: beide 0–19; Gegner 20+, eigene unter 20; eigene 20+, Gegner unter 20; beide 20+. Pro Person/Satz/Match Ass, normal, Fehler, Gesamtzahl und Quoten berechnen. Keine Doppelzählungen.

### 3.3 Aufstellung im Live-Game

- Button **«Aufstellung ansehen»** jederzeit erreichbar. Anzeige der **aktuellen sechs Rotationspositionen**, Nummer, Namen und optionalem Kürzel plus separate Libera.
- **Zusätzlich Feldgrafik in Tiefenperspektive aus Sicht hinter der VBCI-Grundlinie**. Bei Side-out, Spielerwechsel, Rückwechsel, Undo und Redo automatisch aktualisieren. Aktuellen Service auf Position 1 hervorheben, wenn eigenes Team serviert.
- Smartphone: grossflächig, ohne winzige Spielerinnentexte; Laptop: grosszügigere Ansicht. Feldgrafik dient der **schematischen Rotationsdarstellung**, nicht der Behauptung der exakten realen Laufwege während des Ballwechsels.

### 3.4 Spielerwechsel und Rückwechsel

- Button `Spielerwechsel` öffnet **aktuelle sechser Aufstellung**. Person auf Feld wählen → berechtigte Ersatzperson aus dem **Matchkader** auswählen → Wechsel bestätigen; die neue Person übernimmt die richtige Rotationsposition und zukünftige Servicezuordnung. Vorherige statistische Ereignisse bleiben beim ursprünglichen Spieler.
- Regelkonformer **Rückwechsel**: Startspielerin darf, soweit Wettbewerbsregeln dies erlauben, einmal für ihre Ersatzspielerin zurück; Paar danach für weitere reguläre Wechsel gesperrt. Weitere Wechsel- und Rückwechselregeln sowie Teamlimits prüfen; keine pauschale Annahme für alle Alters-/Ligaklassen.
- `Rückwechsel` ist ein echter Spielerwechsel; `Zurück` korrigiert einen irrtümlichen Eintrag. Beides strikt unterscheiden. Libera wird nicht über reguläre Spielerwechsel erfasst.

### 3.5 Vollständige Verlaufsnavigation

- Zwei dauerhaft gut sichtbare Buttons: **`← Zurück` und `Vorwärts →`**, direkt im Score-Bereich.
- Jede bestätigte Spielaktion ist **atomar**: Beim Zurück werden Punkte, eigener/gegnerischer Service, Serviererin, Rotationspositionen, Satzstatus, Spielerwechsel, Normal/Ass/Fehler, Statistiken und UI synchron rekonstruiert. Vorwärts darf nur eine zuvor rückgängig gemachte Aktion wiederherstellen, **niemals neue Ereignisse erzeugen**.
- Am Anfang Zurück deaktivieren, am Ende Vorwärts deaktivieren. Wenn nach Zurück eine neue Aktion erfasst wird, entfällt der alte Redo-Zweig. Zwischenstände persistent speichern, auch nach Browserneustart; unvollständige `Normal`-Eingabe abbrechbar.
- Undo/Redo auch bei Satzendpunkt und Satzvorbereitung korrekt modellieren, ohne vergangene Satzdaten zu beschädigen.

### 3.6 Satzende / Matchende

- Sätze 1–4: Sieg ab **25** mit mindestens **2 Punkten Abstand**, ohne Obergrenze (z. B. 32:30, 34:32). Entscheidungssatz 5: ab **15** mit 2 Abstand.
- Nach Satzende Punkte sperren; **grosse Resultatanzeige**: beide Teams, Endstand, Sieger, Satzstand und Button `Aufstellung Satz X erstellen` für den nächsten Satz.
- Für Satz X neue sechs Namen/Nummern aus **Matchkader**, nicht aus Vor-Satz-Aufstellung. Ersten Aufschlag regelkonform bestimmen; bei Satz 5 neue Auslosung abfragen. Bereits beendete Sätze unverändert lassen.
- Nach **drei gewonnenen Sätzen** zeigt die App den Matchsieger und archiviert mit Status `Abgeschlossen`; bei freiwillig vorzeitigem Beenden Status `Nicht abgeschlossen`. Laufende Spiele können unterbrochen und fortgesetzt werden.

## 4. Screen ARCHIV

- Chronologische Liste: eigenes Team links, Gegner rechts, Datum, Satzresultat, Status `Abgeschlossen` oder `Nicht abgeschlossen`.
- Filter nach Team, Saison, Gegner, Datum und Status. Pausierte laufende Spiele bleiben ausserhalb des Archivs.
- Match-Detail mit historischen Satzresultaten, Startaufstellungen, Spielerwechseln und Statistik pro Spieler/-in, Satz, Match, Team und allen vier Spielphasen. Daten bei späterer Nummernänderung im TEAMS-Screen unverändert.
- Asse, Normal, Fehler, Servicezahl, Assquote, Fehlerquote; bei null Services keine irreführende Prozentzahl. Spieler- und Teamentwicklung über mehrere Spiele, zurückhaltende Diagramme. CSV/JSON-Export; JSON-Backup importierbar, soweit Schema unterstützt.
- Vor endgültigem Löschen klarer Bestätigungsdialog mit Folgen. Kein unbeabsichtigtes Löschen anderer Matches.

## 5. Visuelles Designsystem – VBC Interlaken

- Farben aus Original-Logo: tiefes Nachtblau für Navigation/Headers, klares Volleyball-Blau als Hauptakzent, helles Himmelblau für Panels, Weiss als Grundfläche. Rot ausschliesslich gezielt für Gegner/Fehler, Grün für Erfolg, Rosa für Libera. Gute Lesbarkeit im Tageslicht.
- Einheitliche Tokens für Farben, Abstände, Typografie, Rundungen, Schatten und Animationen. Aufgeräumte Sport-App statt visueller Reizüberflutung.
- Ruhiges **Pulsieren in 1,5–2 Sekunden** am tatsächlich aktiven Servicebereich. Der aktuelle Fokus erhält Animation; andere wichtige Elemente primär über ruhigen Rahmen/Farbe, nicht alles gleichzeitig blinkend. `prefers-reduced-motion`: Animation stoppen, statische Kennzeichnung behalten.
- Aktive Eingabe deutlich markieren, Satzende prominent und nicht störend. Responsives Layout für Hochformat und Desktop. Bottom Navigation auf Smartphones fest, sichere Abstände bei Notches.
- **Feldgrafik:** Perspektive von **hinter der Grundlinie des eigenen Teams**; perspektivisch kleiner werdendes Vorderfeld am Netz; klare Linien und Name/Nummer auf allen sechs Positionen. Positionen: Netzseite `4 / 3 / 2`, hintere Reihe `5 / 6 / 1`; Libera ausserhalb der sechs Positionen separat. Die Grafik muss auf Smartphone auch bei kleiner Breite lesbar bleiben. Datengetriebene Anzeige, keine hartcodierten Beispieldaten.

## 6. Architektur, Migration und GitHub Pages

- Browser-Web-App, statisch auf GitHub Pages lauffähig (keine Secrets im Client). HTML/CSS/JS oder entsprechender statischer Build. Dateien `index.html`, `app.js`, `style.css`, `logo.png`, `manifest.webmanifest`, `icon.svg`, `README.md`, dieser Masterprompt direkt ins Root-Repository.
- Konsistente, versionierte Datenstruktur für Vereins-/Team-ID, Saison, Person-ID, Match-Snapshot, Satz-Startaufstellung, aktuelle Rotation, Serviceaktionen und Event-Historie. Historische Spielerdaten unveränderlich.
- Lokaler Browser-Speicher pro Gerät; automatisches Speichern; Daten-Export/Import als Backup und verständliche Warnung, dass Browserdaten durch Speicherlöschung verloren gehen können. **Kein** angeblicher Cloud-Sync zwischen Geräten.
- Bei App-Updates bestehende gespeicherte Daten **migrieren statt löschen**, Speicher-Key kompatibel halten. Eingaben validieren, kritische Aktionen absichern. Offline-Nutzung nur dann garantieren, wenn entsprechende PWA-Cache-Mechanik tatsächlich umgesetzt und geprüft wurde.

## 7. Abnahmekriterien und Tests

1. Alle vier Navigationslabels exakt und korrekt sortiert.
2. Vorhandene Teams und neue Teams klar getrennt; Kader team-/saisonbezogen.
3. Nummernänderung in TEAMS verändert weder laufende noch archivierte Matches; zukünftige Matches übernehmen neue Nummer.
4. In `Neues Spiel > Spieldaten` **kein Spielort und keine Erstservice-Auswahl**.
5. In `Neues Spiel > Aufstellung` 1. Service exklusiv auswählbar und bestätigt.
6. Matchkader übernimmt zunächst **alle aktiven** Personen; Personen abwählbar.
7. Aufstellung Satz 2–5 unabhängig aus Matchkader; automatische Namensauflösung, doppelte Nummern gesperrt.
8. Aufstellung sowohl im Aufstellungsschritt als auch live aus Trainerperspektive **hinter der Grundlinie** sichtbar; exakt 4/3/2 und 5/6/1.
9. Eigener Service: Ass / Normal (+ Ergebnis) / Fehler korrekt; Gegner-Ansicht bleibt nach gegnerischem Punkt.
10. Side-out rotiert exakt einmal, zeigt **sofort** richtige neue Aufschlagperson (Nummer, Name, optional Kürzel).
11. Gegner-Punktebutton rechts unter Gegner, eigener links unter eigenem Team.
12. Spielerwechsel und regelkonformer Rückwechsel; Libera als separate Anzeige.
13. Undo/Redo über Side-out, Spielerwechsel, Satzende konsistent; nach Zurück + neuer Aktion Redo-Zweig deaktiviert.
14. Satzende bei 25:23, 26:24, 32:30, 34:32 und Entscheidungssatz 15:13; bei 25:24 weiterspielen.
15. Statistik und Vier-Phasen-Auswertung stimmen auch nach Korrekturen und Archivierung.
16. Daten nach Neuladen erhalten; JSON-Backup und CSV-Export funktionieren.
17. Smartphone und Laptop getestet, Fokusanimation unaufdringlich, reduzierte Bewegung respektiert.

**Umsetzungsdisziplin:** Bei jeder Release explizit zwischen **in Code vorhanden**, **getestet** und **nur spezifiziert** unterscheiden. Zielumfang nicht als implementiert behaupten. Keine Veränderung historischer Daten durch UI-Anpassungen.
