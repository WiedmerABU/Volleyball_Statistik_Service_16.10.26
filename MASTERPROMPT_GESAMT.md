# VBC Interlaken – Gesamt-Masterprompt für die Service-Statistik-App

**Version:** 1.0 · **Ziel:** responsive, GitHub-Pages-fähige Web-App · **Sprache:** Deutsch (Schweiz)

## A. Produktauftrag und Entwicklungsregeln

Entwickle eine professionelle, besonders schnell und intuitiv bedienbare Volleyball-Service-Statistik-App für Smartphone, Tablet und Laptop. Schwerpunkt ist die Erfassung **jedes eigenen Aufschlags**, nicht eine vollständige allgemeine Spielstatistik. Verwende das zur Verfügung gestellte VBC-Interlaken-Logo als Gestaltungsvorlage mit seriöser, moderner Typografie, klaren Kontrasten und ruhigen Animationen. Logo nicht verfälschen.

- Die vier Hauptscreens heissen **exakt und in dieser Reihenfolge:** `Teams | Neues Spiel | Live-Game | Archiv`.
- Mobile: dauerhaft sichtbare, sichere Bottom Navigation (Safe Areas beachten); Desktop: angepasste Navigation. Aktiver Screen hervorgehoben.
- Eigenes Team **immer links**, Gegner **immer rechts**, auch beim Servicewechsel.
- Bedienflächen fingerfreundlich, minimaler Klickaufwand, fokussierte grosse Ansicht. Wechsel zwischen Screens darf keinen abgeschlossenen Spielzustand verlieren.
- Spielaktionen müssen atomar verarbeitet werden; Punkte, Serviceereignis, Rotation und Rückgängig dürfen sich nicht widersprechen.
- Saubere Trennung von UI, Domänenlogik, Persistenz und Statistik. Semantische, barrierearme Bedienelemente; sichtbare Statusanzeige zusätzlich zu Farben; reduzierte Bewegung respektieren.
- Bei Unklarheiten (z. B. Spezialregeln einer Nachwuchsliga) vor der Implementierung gezielt nachfragen. Nie stillschweigend Spielregeln erfinden.

## B. Screen 1 – TEAMS

### B1 Verein und Saison
- Verein als Pflichtfeld erfassen, gespeicherte Vereine wieder auswählen, mehrere Mannschaften pro Verein verwalten.
- Saison frei erfassen oder auswählen, etwa `2026/27`. Mannschaft und Teamkader eindeutig der Saison zuordnen.
- Zwischen Mannschaften wechseln. Automatisch beschriftete Mannschaften anhand von Verein, Kategorie, Liga/Altersklasse, optionaler Gruppe und Saison.

### B2 Kategorie und optionale Gruppe

| Kategorie | Auswahl | Gruppe |
|---|---|---|
| Damen | 1.–5. Liga | A, B, C, D **optional nur in 3.–5. Liga** |
| Herren | 1.–4. Liga | A, B, C, D **optional nur in 3.–4. Liga** |
| Mixed | keine Liga | keine |
| Juniorinnen | U14, U16, U18, U20, U23 | keine |
| Junioren | U14, U16, U18, U20, U23 | keine |

Nicht benötigte Felder dynamisch ausblenden und alte unpassende Werte zurücksetzen. Gruppe ist keine Pflichtangabe und nicht für alle Meisterschaften vorhanden.

### B3 Kader
- Pflicht: Rückennummer `0–99`, Vorname, Nachname. Freiwillige Standard-Spielrolle: `P` Passeuse, `A` Aussen, `M` Mitte, `D` Diagonal, `L` Libera/Libero oder keine.
- Eingabe: schmale Nummernspalte, daneben Vorname, darunter Nachname; Zahlentastatur auf Smartphones.
- Nach Rückennummer sortieren, Nummern innerhalb des aktiven Kaders eindeutig halten. Unbegrenzter Saisonkader, Matchkader getrennt.
- Hinzufügen, bearbeiten, deaktivieren/reaktivieren, Nummer und Rolle ändern; komplette Mannschaft als Ausgangsbasis in neue Saison übernehmen und anpassen.
- Dauerhafte Spieler-IDs und historische Datenschnappschüsse: weder Deaktivierung noch neue Trikotnummern dürfen alte Spielstatistiken ändern.
- Lokale Speicherung und JSON-Export/Import mit Formatversion, Validierung und Sicherheitsabfrage beim Überschreiben.

## C. Screen 2 – NEUES SPIEL

### C1 Spieldaten
- Bestehende Mannschaft links, Gegner rechts, Gegnername und Datum erforderlich; Spielort optional.
- Unter jedem Team ein **exklusiver** Button zur Festlegung `1. Service eigenes Team` oder `1. Service Gegner` für Satz 1; keine stille Vorauswahl.
- Hauptbutton **«Spiel eröffnen» über die gesamte Breite**. Incomplete Vorbereitung zuerst fertigführen; keine doppelten Matches durch mehrmaliges Tippen.

### C2 Matchkader
- Aktive Personen aus gewähltem Teams-Kader auswählen; Anzahl sichtbar. Pro Match bis zu **zwei zusätzliche** Spieler/-innen temporär ergänzen.
- Pro Person Nummer, Name, optional Rolle (`P/A/M/D/L`); Rolle ist im Match veränderbar ohne Stammdaten/alte Statistiken zu überschreiben.
- Mindestens sechs reguläre Startspieler/-innen; mögliche Wettkampfgrenzen und Sonderregeln konfigurierbar.

### C3 Aufstellungszettel pro Satz
- Sechs Rotationspositionen im Schiedsrichter-Aufstellungszettel-Stil, mit Namen und Nummern **aller sechs**. Netz oberhalb der ersten Zeile:

```text
       NETZ
    4   3   2
    5   6   1
    L           (nur separate Anzeige, keine siebte Rotation)
```

- Pro Satz (1–5, jeweils nur wenn benötigt) werden die **sechs Nummern direkt aus dem Matchkader** neu eingetragen/ausgewählt; **keine automatische Übernahme der Startaufstellung des vorherigen Satzes**.
- Beim Auswählen Namen und zuletzt für diesen Match festgelegte Rollen automatisch ergänzen. Rolle änderbar.
- Doppelte, unbekannte, nicht berechtigte oder als Libera deklarierte reguläre Startnummern verhindern. Erst nach vollständiger Prüfung mit **«Aufstellung bestätigen»** speichern. Vorherige Sätze bleiben unverändert.
- Libera separat in **Spalte 1/Zeile 3**, optisch hervorgehoben, mit Nummer und Name; keine eigene Libera-Einsatzverwaltung, kein Service-Button für Libera. Eine rein visuelle Libera-Karte ersetzt nicht die FIVB-konforme Erfassung realer Libera-Wechsel – entsprechende Einschränkung dokumentieren.
- Nach Satzende nächsten Satz aus Matchkader vorbereiten. Satzfolge beim ersten Service gemäss Wettbewerbsregeln; vor Satz 5 neue Auslosung abfragen.

### C4 Laufende Spiele
- Noch nicht fertiggestellte, nicht archivierte Spiele mit Gegner, Datum, Satz, Satz-/Punktestand und Aktionen **Fortsetzen** bzw. **Vorzeitig archivieren («Nicht abgeschlossen»)**.
- Kein neues Spiel darf ein laufendes überschreiben. Entwürfe bei Bedarf gesondert speichern.

## D. Screen 3 – LIVE-GAME

### D1 Spielbeginn und zentrale UI
- Bei Satz 1 unmittelbar die beim Erstellen festgelegte Ansicht öffnen: `1. Service [eigene Mannschaft]` oder `1. Service Gegner`. Danach dynamische Serviceanzeige.
- Punktestände sichtbar: links eigenes Team, rechts Gegner; deutliche Trennung.
- **Bei eigenem Aufschlag** grosse Karte der Aufschlagspielerin auf Rotationsposition 1 mit **grosser Trikotnummer, vollem Namen und optionalem Spielrollenkürzel**; sanft pulsierender blauer Rahmen. Aktionen: **Ass | Normal | Fehler**.
- **Bei gegnerischem Aufschlag** grosse Zweispalten-Punkteansicht: grüner **«+ Punkt» direkt unter dem eigenen Team links**, roter **«+ Punkt» direkt unter dem Gegner rechts**. Gegnerbereich pulsiert rot. Keine seitenbreiten gemeinsamen Punktebuttons.
- Immer sichtbares «Rückgängig»; unwichtige Verwaltungsfunktionen in aufklappbare Bereiche. Vollbild-Fokusoption und klare, fingerfreundliche Abstände.

### D2 Ballwechsel-/Service-Zustandsmaschine
- **Ass (eigener Service):** eigenes Team +1; ein Ass-Ereignis, selbe Spielerin serviert erneut; keine Rotation.
- **Fehler (eigener Service):** Gegner +1; ein Fehler-Ereignis; Gegner übernimmt Aufschlagrecht; sofort Gegneransicht, **keine eigene Rotation**.
- **Normal (eigener Service):** zunächst offener Service-Vorgang; anschliessend zwingend zwei Ergebnisbuttons: **Punkt eigenes Team** → eigenes Team +1, derselbe Server bleibt; **Punkt Gegner** → Gegner +1, Aufschlagrecht Gegner. Genau **ein** normales Serviceereignis nach Ergebnisbestätigung erfassen.
- **Gegner serviert, Gegnerpunkt:** Gegner +1 und Gegneransicht unverändert.
- **Gegner serviert, eigener Punkt (Side-out):** eigenes Team +1, **genau eine eigene Rotation**, bisherige Position 2 wird Position 1; unmittelbar eigene grosse Serviceansicht mit neuer Nummer, Name, optionalem Kürzel. Ohne Zwischenbildschirm.
- Eigene Rotation beim Side-out `2→1→6→5→4→3→2`. Keine Rotation nach eigener Service-Serie oder verlorenen Ballwechseln am eigenen Service.
- Doppeltaps gegen doppelte Punkte/Rotation schützen; unvollständige Normaleingaben vor Navigation sichern oder korrekt unterbrechen.

### D3 Statistiken
- Jedes eigene Serviceereignis erhält Spieler-ID, Satz, Art, Ausgangspunktestand **vor dem Service**, Ballwechselgewinner und Zeit/Reihenfolge; ass + normal + fehler = Servicegesamtzahl.
- Vier exklusive Phasen: **(1)** beide 0–19, **(2)** eigenes Team 0–19 / Gegner ≥20, **(3)** eigenes Team ≥20 / Gegner 0–19, **(4)** beide ≥20.
- Spieler-, Satz-, Match- und Teamstatistik; Assquote, Fehlerquote, Service-Serien. Null-Division vermeiden.

### D4 Spielsteuerung
- Spielerwechsel einfach aus regulärem Matchkader; Statistik bleibt bei der tatsächlichen Aufschlagspielerin. Regeln zur Zahl und Art von Wechseln für die jeweilige Liga prüfen/konfigurieren. Libera bleibt nur separate Anzeige.
- Reguläre Sätze mindestens 25, Entscheidungssatz mindestens 15 Punkte, jeweils 2 Differenz; Satzgewinner erkennen, Eingaben sperren, nächste Satzaufstellung bestätigen. Match nach 3 Gewinnsätzen abgeschlossen.
- Pausieren/Fortsetzen, vorzeitig ins Archiv mit Status «Nicht abgeschlossen» (Bestätigung), normales Ende als «Abgeschlossen».
- Rückgängig nimmt den **gesamten letzten Zustandswechsel atomar** zurück: Punkt, Serviceaktion, Aufschlagrecht, Rotation, Wechsel und Statistik.
- Nach jeder abgeschlossenen Aktion persistent speichern; Browser-Neuladen muss Spiel wiederherstellen.

## E. Screen 4 – ARCHIV

- Kartenliste abgeschlossener und vorzeitig archivierter Spiele; pausierte Matches verbleiben unter «Laufende Spiele». Filter nach Verein/Mannschaft, Saison, Gegner, Zeitraum, Status.
- Matchdetails: eigene Mannschaft links, Gegner rechts, Satzresultate, damals gespeicherter Matchkader und Aufstellungszettel je Satz.
- Eigene Serviceauswertung pro Satz, Match, Person und Mannschaft; Kennzahlen Asse, Normal, Fehler, Services, Assquote und Fehlerquote; vier Spielphasen.
- Historische Entwicklung über mehrere Matches und Saisons, Spieler-/Teamauswertungen, einfache Diagramme; Teilmatches optional in Aggregation ein-/ausschliessen.
- Export CSV (Excel-kompatibel) und JSON (versioniert); spätere PDF-Berichte optional.
- Löschen nur mit Bestätigung und Hinweis auf vollständigen Statistikverlust dieses Matches. Kein historischer Datensatz darf durch Team- oder Namensänderungen verfälscht werden.

## F. Architektur, Tests, GitHub

- Statische Web-App ohne notwendigen Backendserver, GitHub Pages `main` / `root` nutzbar; relative Assetpfade, mobile Manifest-Einbindung.
- Eine gemeinsame zentrale Datenstruktur mit stabilen IDs und unveränderlichen Match-Snapshots. IndexedDB für Zielversion bevorzugt; formatversionierte JSON-Sicherung. **Browserlokale Speicherung synchronisiert nicht automatisch zwischen Geräten.**
- Für Update/Migration lokale Bestandsdaten respektieren; existierende Datensätze niemals ohne bestätigte Migration überschreiben.
- Zustandsmaschine für Rallys, Service und Satzende getrennt von DOM/UI. Jede Aktion besitzt Validierung, Protokollierung und Undo-Snapshot.
- Abnahmetests: Mannschaft/Gruppe/Kader, mehrere Saisons, gültiger Spielbeginn von beiden Seiten, Side-out-Reihenfolge, Services aller drei Arten, Satzwechsel mit neuer Matchkader-Aufstellung, Entscheidungssatz, Spielerwechsel, Rückgängig, Reload, Archiv, JSON/CSV-Export und historische Unveränderlichkeit.
- Dokumentiere Implementierungsstand ehrlich; keine vollständige Regelkonformität behaupten, solange liga- und liberaspezifische Sonderfälle nicht getestet sind.

## G. Release- und Lieferumfang

Liefere die vollständigen statischen Dateien `index.html`, `style.css`, `app.js`, `manifest.webmanifest`, `icon.svg`, `logo.png` sowie `README.md` und diese Spezifikation. Keine Dateien in versteckten Build-Ordnern. Vor Übergabe Syntax, Navigation, Browser- und Mobilansicht testen.

**Priorität:** schnelle, zuverlässige, intuitive Live-Serviceerfassung vor dekorativen Zusatzfunktionen.
