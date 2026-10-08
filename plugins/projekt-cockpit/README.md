# Projekt-Cockpit

Ein persönliches Projekt-Cockpit für Claude: alle Projekte über mehrere Firmen auf einer Seite, mit Fortschritt als Tacho, Tagesbriefing, Fristen, abhakbaren Aufgaben mit Wiedervorlage, Kalender und Volltextsuche. Das Cockpit entsteht als privates claude.ai-Artifact im eigenen Konto und wird werktags automatisch aktualisiert.

## Skills

| Skill | Wofür |
| --- | --- |
| cockpit-einrichten | Sammelt die Projekte aus Claude-Unterhaltungen, Projekt-Tracker und Kalender, veröffentlicht das Cockpit und richtet die tägliche Aktualisierung ein. Beispiel: „Richte mein Projekt-Cockpit ein.“ |
| cockpit-aktualisieren | Frischt die Daten auf und nimmt abgehakte und gelöschte Aufgaben heraus. Beispiel: „Aktualisiere mein Cockpit.“ |

## Funktionen des Cockpits
- Tacho je Projekt und Gesamt-Tacho, Kontrollleuchten für Blockiert, Gefährdet, Fristen ≤ 7 Tage, Im Plan
- Tagesbriefing „Heute wichtig“ und Fristen mit Countdown
- Aufgaben abhaken, löschen (mit Rückgängig) oder auf Wiedervorlage legen
- Monatskalender mit Kalender-Terminen (live, nur lesend), Fristen, Wiedervorlagen und eigenen Terminen (anlegen, bearbeiten, löschen)
- Suche über alle Projektdaten, Aufgaben, Fristen und Termine
- Aktualisieren-Knopf und automatische Aktualisierung alle 15 Minuten
- Hell- und Dunkelmodus, nutzbar ab Handybreite

## Voraussetzungen
- Claude-Plan mit Artifacts, Cowork-Desktop-App für die geplante tägliche Aktualisierung
- Optional: Kalender-Connector (getestet mit Microsoft 365) und Projekt-Tracker-Connector (getestet mit Asana), siehe CONNECTORS.md

## Datenschutz
Projektdaten liegen ausschließlich im claude.ai-Konto der Person: in der Datei data.json des eigenen Artifacts und in dessen Datenbank (Häkchen, Wiedervorlagen, eigene Termine). Das Plugin sendet keine Daten an Dritte. Kalendertermine werden über den eigenen Connector nur gelesen. Das Artifact ist privat, bis die Person es selbst teilt.

## Lizenz
MIT, siehe LICENSE.
