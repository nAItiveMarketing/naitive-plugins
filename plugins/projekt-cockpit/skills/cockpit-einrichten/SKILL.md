---
name: cockpit-einrichten
description: Richtet ein persönliches Projekt-Cockpit als privates claude.ai-Artifact ein – Tacho je Projekt, Tagesbriefing, Fristen, abhakbare Aufgaben mit Wiedervorlage, Kalender und Suche. Verwenden, wenn jemand sagt „richte mein Projekt-Cockpit ein“, „baue mir ein Projekt-Dashboard über alle meine Projekte“, „Cockpit für meine Projekte erstellen“ oder ein bestehendes Cockpit neu aufsetzen will.
---

# Projekt-Cockpit einrichten

Ziel: ein privates Artifact mit der Vorlage `assets/index.html` und einer eigenen `data.json` mit den echten Projekten der Person veröffentlichen, plus eine tägliche Aktualisierung einrichten.

## 1. Klären (kurz, gebündelt)
Frage nur, was nicht schon bekannt ist:
- Welche Firmen/Bereiche gehören ins Cockpit? (wird `company`)
- Woher kommen die Projekte? Claude-Unterhaltungen, Projekt-Tracker (~~project tracker), Kalender (~~calendar), E-Mail.
- Kopfzeile, z. B. „Name · alle Firmen“ (wird `owner`).
- Soll werktags automatisch aktualisiert werden, und um welche Uhrzeit?

## 2. Daten sammeln
- Claude-Unterhaltungen: `list_sessions` und `read_transcript` (bei vielen Unterhaltungen parallel über Subagenten). Je Vorhaben ein Projekt; einmalige Fragen ohne offenen Punkt weglassen.
- Projekt-Tracker: Projekte und Aufgabenzählung; Fortschritt = erledigt / gesamt.
- Nichts erfinden. Fortschritt bei Projekten aus Unterhaltungen ist eine begründete Schätzung; Begründung in `progressNote`.
- Feldbeschreibung: `references/datenmodell.md`. Struktur-Beispiel: `assets/data.example.json` (nur Beispiel, nie veröffentlichen).

## 3. Veröffentlichen
1. `assets/index.html` unverändert in den Arbeitsordner kopieren.
2. `data.json` schreiben und prüfen: gültiges JSON, alle `briefing.items[].project` und `deadlines[].project` verweisen auf vorhandene IDs, `lastActivity` überall gesetzt.
3. Mit dem Artifact-Werkzeug veröffentlichen: `file_path` = index.html, `files` = {"data.json": <Pfad>}, `icon` = "gauge".
4. Beim ersten Veröffentlichen die Fähigkeiten deklarieren (vorher den Skill `artifact-capabilities` laden):
   `{"db": {}, "user": {}, "mcp": {"servers": [{"server": "<Anzeigename des Kalender-Connectors, z. B. Microsoft 365>", "tools": ["outlook_calendar_search"]}]}}`
   Ohne Kalender-Connector `mcp` weglassen – die Seite zeigt dann nur Fristen, Wiedervorlagen und eigene Termine.
5. Hinweis an die Person: Beim ersten Öffnen Datenbank- und Kalenderzugriff erlauben. Oben rechts zeigt die Seite, ob Häkchen geräteübergreifend gespeichert werden und ob der Kalender verbunden ist.

## 4. Tägliche Aktualisierung
Mit dem Werkzeug für geplante Aufgaben eine werktägliche Aufgabe anlegen, deren Prompt den Skill `cockpit-aktualisieren` mit der Artifact-URL aufruft. Darauf hinweisen, dass sie nur läuft, wenn die Claude-App geöffnet ist.

## Regeln
- Die Vorlage nicht umbauen; Inhalte nur über `data.json` ändern.
- Keine Daten anderer Personen oder Firmen übernehmen, die nicht zur Person gehören.
- Bei späteren Veröffentlichungen KEIN `capabilities`-Feld mitschicken (es würde die gespeicherten ersetzen).
- Texte auf Deutsch, kurz und konkret.
