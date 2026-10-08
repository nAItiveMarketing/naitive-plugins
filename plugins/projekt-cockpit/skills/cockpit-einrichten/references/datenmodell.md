# Datenmodell Projekt-Cockpit

## data.json – oberste Ebene
| Feld | Typ | Bedeutung |
| --- | --- | --- |
| owner | Text | Kopfzeile über dem Titel, z. B. „Name · alle Firmen“ |
| updated | ISO-Zeit mit Offset | Datenstand |
| coverage | Text | welche Quellen geprüft wurden (1 Satz) |
| calendarHide | Liste Text | Betreff-Teile, deren Kalendertermine ausgeblendet werden |
| briefing.date | YYYY-MM-DD | Tag des Briefings |
| briefing.headline | Text | 1–2 Sätze, worauf es heute ankommt |
| briefing.items[] | {prio, project, text} | „Heute wichtig“; prio = hoch, mittel, niedrig; project = Projekt-ID |
| briefing.deadlines[] | {date, text, project} | Fristen |
| projects[] | Objekt | siehe unten |

## data.json – je Projekt
| Feld | Typ | Bedeutung |
| --- | --- | --- |
| id | Text, kebab-case | stabiler Schlüssel, nie ändern |
| name | Text | Projektname |
| company | Text | Firma/Bereich (Filter-Chips) |
| source | „Claude“ oder Tracker-Name | Herkunft des Fortschritts |
| progress | 0–100 | Tacho |
| progressNote | Text | Begründung des Fortschritts |
| status | on-track, at-risk, blocked, paused, done | Statusfarbe, Kontrollleuchten |
| summary | Text | Kurzstand, 1–2 Sätze |
| nextSteps | Liste Text, max. 3 | abhakbar |
| openItems | Liste Text | weitere offene Punkte, abhakbar |
| details | Text | Fakten, Namen, Beträge, Dateien; durchsuchbar |
| sources | Liste Text | Titel der Unterhaltungen/Artifacts |
| lastActivity | YYYY-MM-DD | „Zuletzt aktiv“, nie leer |

## Artifact-Datenbank (wird von der Seite geschrieben)
| Sammlung | Dokument-ID | Felder |
| --- | --- | --- |
| items | `<Projekt-ID>~<Hash des Texts>` | project, text, state (done, deleted, snoozed), until, at |
| events | `ev-…` | title, date, endDate, allDay, time, endTime, project, note, at |

Aufgaben werden über Projekt-ID + exakten Wortlaut erkannt. Umformulieren löst die Verknüpfung zu Häkchen und Wiedervorlagen.

## Seite (index.html)
- Kalender-Connector: die Seite ruft `outlook_calendar_search` über den Connector mit dem Anzeigenamen „Microsoft 365“ auf. Bei einem anderen Connector-Namen den Namen in `callOutlook()` anpassen.
- Neue Datenquellen mit `onRefresh(name, fn)` anmelden; sie laufen dann beim Start, beim Klick auf „Aktualisieren“ und alle 15 Minuten.
- Neue durchsuchbare Felder in `projText()` ergänzen.
