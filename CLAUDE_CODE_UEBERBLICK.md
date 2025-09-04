# Claude Code – Überblick und Schnellstart

## Was ist Claude Code?
Claude Code ist ein KI-gestützter Entwicklungsassistent für dein Terminal/Editor (z. B. Cursor), der natürliche Sprache mit Code-Verstehen verbindet. Er kann Code analysieren, ändern, testen, dokumentieren und Aufgaben automatisieren. Mit Subagents lassen sich spezialisierte Arbeitsabläufe kapseln.

## Installation
- Stelle sicher, dass Node.js >= 18 installiert ist.
- Installiere das CLI global:
```bash
npm install -g @anthropic-ai/claude-code
```

## Start im Projekt
```bash
cd /path/to/your/project
claude
```
- Starte eine Sitzung und beschreibe deine Aufgabe in natürlicher Sprache, z. B.:
  - „Erkläre mir die Architektur dieses Repos.“
  - „Füge eine Funktion hinzu, die X berechnet, inkl. Tests.“

## Typische Workflows
- **Code-Verständnis**: Fragen zu Architektur, Abhängigkeiten, Datenfluss
- **Editieren & Refactoring**: Änderungen vorschlagen lassen und direkt anwenden
- **Debugging**: Fehlermeldungen einkopieren, Ursache und Fix planen lassen
- **Tests & QA**: Tests erzeugen/ausführen, Fehler beheben, Performance/Accessibility prüfen
- **Git-Integration**: Änderungen diffen, commiten, Branches/Pull Requests vorbereiten

## Nützliche Befehle (Beispiele)
- „Was hat sich in den letzten Commits geändert?“
- „Refactore `utils/date.ts` und erhöhe die Testabdeckung.“
- „Erstelle Release Notes aus dem Git-Log.“

## Subagents (kurzer Vorgeschmack)
Subagents sind spezialisierte KI-Helfer mit eigener Beschreibung, eigenen Tools und eigenem Systemprompt. Sie können projektweit oder benutzerweit verfügbar sein und gezielt für Aufgaben wie Code-Review, Accessibility-Checks oder Security-Scans genutzt werden.

Mehr dazu in `AGENTS_UND_SUBAGENTS_ANLEITUNG.md`.

