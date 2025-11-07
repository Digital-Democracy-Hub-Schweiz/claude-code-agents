# claude-code-agents
Unsere fleissigsten Mitarbeitenden

## Claude Code – Überblick und Schnellstart

### Was ist Claude Code?
Claude Code ist ein KI-gestützter Entwicklungsassistent für dein Terminal/Editor (z. B. Cursor), der natürliche Sprache mit Code-Verstehen verbindet. Er kann Code analysieren, ändern, testen, dokumentieren und Aufgaben automatisieren. Mit Subagents lassen sich spezialisierte Arbeitsabläufe kapseln.

### Installation
- Stelle sicher, dass Node.js >= 18 installiert ist.
- Installiere das CLI global:
```bash
npm install -g @anthropic-ai/claude-code
```

oder prüfe, ob ein Update verfügbar ist mit: 
```bash
claude update
```

### Start im Projekt
```bash
cd /path/to/your/project
claude
```
- Starte eine Sitzung und beschreibe deine Aufgabe in natürlicher Sprache, z. B.:
  - „Erkläre mir die Architektur dieses Repos.“
  - „Füge eine Funktion hinzu, die X berechnet, inkl. Tests.“

### Typische Workflows
- **Code-Verständnis**: Fragen zu Architektur, Abhängigkeiten, Datenfluss
- **Editieren & Refactoring**: Änderungen vorschlagen lassen und direkt anwenden
- **Debugging**: Fehlermeldungen einkopieren, Ursache und Fix planen lassen
- **Tests & QA**: Tests erzeugen/ausführen, Fehler beheben, Performance/Accessibility prüfen
- **Git-Integration**: Änderungen diffen, commiten, Branches/Pull Requests vorbereiten

### Nützliche Befehle (Beispiele)
- „Was hat sich in den letzten Commits geändert?“
- „Refactore `utils/date.ts` und erhöhe die Testabdeckung.“
- „Erstelle Release Notes aus dem Git-Log.“


## Nützliche Tipps mit Claude Code: 

### 1. Initialisieren
Initialisiere Claude Code in einem Projekt

```bash
claude
/init
```
erstellt eine Datei "CLAUDE.md" anhand der vorgegebenen Projektstruktur

### 2. Session Management 
Du kannst mit folgendem Befehl eine alte Session wiederherstellen. 
```bash
claude --resume
```

### 3. Bash Commands & Permissions
In Claude Code können auch verschiedene Commands verwendet werden.
![Claude Code Permissions](/pictures/permissions.png)
Nützliche Commands sind: 
- git add:*
- git commit:*
- git push:*
- cat:*
- ls:*
- curl:*

### 4. Todo Listen
Gib Claude Code den Auftrag einen Plan zu erstellen, wie die Aufgabe gelöst werden soll. Das hilft vor allem bei grösseren Code Aufgaben die Qualität von Claude Code zu gewährleisten. 

```text 
Let's build an MVP of the webapp described in docs/mvp_concept.md. Frist, let's create an engineering implementation plan for the MVP features. Output it in docs/mvp_eng.plan.md
```

### 5. Dokumentationen
verwenden in Claude den folgenden Befehl: 
```text 
Explore project and help me understand the strcuture and workflows of the app. Save your findings in a markdown file in the folder /docs.
```



### Subagents (kurzer Vorgeschmack)
Subagents sind spezialisierte KI-Helfer mit eigener Beschreibung, eigenen Tools und eigenem Systemprompt. Sie können projektweit oder benutzerweit verfügbar sein und gezielt für Aufgaben wie Code-Review, Accessibility-Checks oder Security-Scans genutzt werden.

## Agents und Subagents mit Claude Code – Erstellung und Verwaltung

Diese Anleitung zeigt, wie du mit Claude Code spezialisierte Agents/Subagents für wiederkehrende Aufgaben (z. B. Accessibility-Tests und -Fixes) erstellst, konfigurierst und einsetzt.

### Begriffe
- **Agent**: Allgemeiner KI-Assistent in deiner Sitzung.
- **Subagent**: Spezialisierter Assistent mit eigener Beschreibung, eigenem Systemprompt und optional eingeschränktem Tool-Zugriff.

### Vorteile
- **Spezialisierung**: Bessere Trefferquote für bestimmte Aufgaben
- **Kontexttrennung**: Eigene Kontexte entlasten die Hauptkonversation
- **Wiederverwendung**: Einmal definieren, projekt- oder benutzerweit nutzen
- **Sicherheit**: Tools/Berechtigungen fein granular vergeben

### Erstellen eines Subagents
1. Starte Claude Code im Projekt:
   ```bash
   claude
   ```
2. Öffne die Subagent-Verwaltung:
   ```
   /agents
   ```
3. Wähle „Create New Agent“ und fülle die Felder aus:
   - **Name**: Kurz, prägnant (z. B. `accessibility-tester`)
   - **Beschreibung**: Was dieser Subagent tut und wann er einzusetzen ist
   - **Systemprompt**: Klare, dauerhafte Leitplanken (z. B. WCAG-Referenzen, Output-Format)
   - **Tools**: Explizit erlaubte Tools wählen (oder leer lassen, um Standard zu erben)
   - **Sichtbarkeit**: Projektweit oder benutzerweit (siehe Speicherorte unten)
4. Speichern. Der Subagent ist nun verfügbar.

### Nutzung
- Automatisch: Claude Code kann passende Subagents vorschlagen/nutzen.
- Explizit anfordern, z. B.:
  ```
  Verwende den `accessibility-tester` Subagent, um aktuelle Accessibility-Probleme zu reporten.
  ```

### Speicherorte und Versionierung
- **Projekt-Subagents**: `.claude/agents/` im Repo (können eingecheckt und geteilt werden)
- **Benutzer-Subagents**: `~/.claude/agents/` (nur lokal, gelten über Projekte hinweg)
- Bei Namenskonflikten hat das Projekt Vorrang.

### Best Practices für Subagents
- **Glasklare Ziele**: Eine Aufgabe, klar definierte Outputs (Markdown-Report, JSON o. ä.)
- **Determinismus erhöhen**: Formatvorgaben, Schrittpläne, Abbruchkriterien
- **Tool-Scope minimieren**: Nur benötigte Tools freischalten
- **Qualitätssicherung**: Subagent-Ergebnisse von einem zweiten Subagent (Reviewer) oder in CI validieren

### Beispiele (Accessibility)
- `accessibility-reporter`: Fuehrt Lighthouse/WCAG-Checks aus, erstellt Report in `accessibility-reporter.md`.
- `accessibility-fixer`: Liest Reports, implementiert Code-Fixes, ergänzt Tests, dokumentiert Änderungen in `accessibility-fixer.md`.

### Integration ins Team
- Projekt-Subagents im Repo halten und PR-Reviews einführen
- Onboarding: Kurzanleitung in der README, inklusive „Wie rufe ich Subagents auf?“
- CI: Subagents für wiederkehrende QA-Schritte (z. B. Accessibility, Lint, Security)

### Troubleshooting
- Subagent wird nicht gefunden: Namen prüfen, Speicherort korrekt? Sitzung neu starten.
- Fehlende Tools: In der Agent-Konfiguration explizit freischalten.
- Zu vage Ergebnisse: Systemprompt schärfen, Output-Format definieren, Beispiele geben.

## Ressourcen
- PDF-Extrakt: `resources/pdf-extract-accessibility-blog-post.txt`
- Accessibility-Reports: `accessibility-reporter.md`, `accessibility-fixer.md`
