# Connectors

## Wie Tool-Verweise funktionieren

Die Skills nennen Werkzeuge als Kategorie mit `~~`, z. B. `~~calendar`. Gemeint ist der Connector, den die Person in dieser Kategorie in claude.ai verbunden hat. Alle Connectors sind optional; ohne sie arbeitet das Cockpit mit Claude-Unterhaltungen und eigenen Einträgen.

## Connectors für dieses Plugin

| Kategorie | Platzhalter | Getestet mit | Weitere Optionen |
| --- | --- | --- | --- |
| Kalender | `~~calendar` | Microsoft 365 (Outlook) | Google Calendar (Seite anpassen) |
| E-Mail | `~~email` | Microsoft 365 (Outlook) | Gmail |
| Projekt-Tracker | `~~project tracker` | Asana | Linear, Jira, monday.com, ClickUp |

Hinweis: Die Cockpit-Seite fragt den Kalender live über den Connector „Microsoft 365“ ab. Für einen anderen Kalender-Connector den Namen und das Werkzeug in `callOutlook()` der Vorlage anpassen.
