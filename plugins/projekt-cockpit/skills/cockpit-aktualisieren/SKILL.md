---
name: cockpit-aktualisieren
description: Aktualisiert die Daten eines bestehenden Projekt-Cockpits (data.json) aus Claude-Unterhaltungen, Projekt-Tracker, Kalender und E-Mail und berücksichtigt abgehakte, gelöschte und auf Wiedervorlage gelegte Aufgaben. Verwenden bei „aktualisiere mein Cockpit“, „Cockpit-Daten auffrischen“, „trag X im Cockpit nach“ oder wenn eine geplante Aufgabe das Cockpit aktualisieren soll.
---

# Projekt-Cockpit aktualisieren

Eingabe: die claude.ai-URL des Cockpit-Artifacts. Fehlt sie, mit dem Artifact-Werkzeug (`action: list`) nach „Projekt-Cockpit“ suchen oder nachfragen.

## Ablauf
1. **Status der Aufgaben lesen:** ArtifactData `list` auf der Sammlung `items` (query.limit 1000, weiter per cursor). Felder: project, text, state (`done`, `deleted`, `snoozed`), until. Nicht verändern. Sammlung `events` (eigene Termine) nur lesen.
2. **Daten lesen:** Artifact `read` mit `path: "data.json"`, außerdem `path: "index.html"` lokal speichern.
3. **Erledigtes entfernen:** Punkte mit `done` oder `deleted` aus `nextSteps`, `openItems` und `briefing.items` entfernen (Abgleich über Projekt-ID + exakten Text). `snoozed`-Punkte stehen lassen.
4. **Neues einarbeiten:**
   - Claude-Unterhaltungen, die seit `updated` aktiv oder neu sind, vollständig lesen; Stand, Fortschritt, Schritte, Details und Quellen anpassen; neue Vorhaben als neue Projekte anlegen.
   - ~~project tracker: Aufgaben zählen, Fortschritt = erledigt / gesamt, offene Aufgaben als nächste Schritte.
   - ~~calendar und ~~email: heutige Termine und dringende Nachrichten mit Projektbezug für das Briefing. Kalendertermine nicht als Fristen doppeln.
5. **Briefing neu schreiben:** `headline` (1–2 Sätze), 6–10 `items` mit prio hoch/mittel/niedrig, kommende `deadlines`; vergangene entfernen. `updated` = jetzt mit Zeitzonen-Offset.
6. **Prüfen und veröffentlichen:** JSON gültig, alle Projekt-Verweise existieren, `lastActivity` überall gesetzt. Publish auf die URL mit unveränderter index.html und `files: {"data.json": …}` – ohne `capabilities`.
7. **Kurzbericht:** zwei Sätze – was sich geändert hat (inkl. Zahl entfernter Punkte) und was heute am dringendsten ist.

## Wichtig
- Das Cockpit erkennt Aufgaben am exakten Wortlaut. Bestehende Punkte nie umformulieren, sonst gehen Häkchen und Wiedervorlagen verloren.
- Projekt-IDs nie ändern.
- Nichts erfinden; Schätzungen begründen.
- Feldbeschreibung: `../cockpit-einrichten/references/datenmodell.md`.
