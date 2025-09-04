# Agents und Subagents mit Claude Code – Erstellung und Verwaltung

Diese Anleitung zeigt, wie du mit Claude Code spezialisierte Agents/Subagents für wiederkehrende Aufgaben (z. B. Accessibility-Tests und -Fixes) erstellst, konfigurierst und einsetzt.

## Begriffe
- **Agent**: Allgemeiner KI-Assistent in deiner Sitzung.
- **Subagent**: Spezialisierter Assistent mit eigener Beschreibung, eigenem Systemprompt und optional eingeschränktem Tool-Zugriff.

## Vorteile
- **Spezialisierung**: Bessere Trefferquote für bestimmte Aufgaben
- **Kontexttrennung**: Eigene Kontexte entlasten die Hauptkonversation
- **Wiederverwendung**: Einmal definieren, projekt- oder benutzerweit nutzen
- **Sicherheit**: Tools/Berechtigungen fein granular vergeben

## Erstellen eines Subagents
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

## Nutzung
- Automatisch: Claude Code kann passende Subagents vorschlagen/nutzen.
- Explizit anfordern, z. B.:
  ```
  Verwende den `accessibility-tester` Subagent, um aktuelle Accessibility-Probleme zu reporten.
  ```

## Speicherorte und Versionierung
- **Projekt-Subagents**: `.claude/agents/` im Repo (können eingecheckt und geteilt werden)
- **Benutzer-Subagents**: `~/.claude/agents/` (nur lokal, gelten über Projekte hinweg)
- Bei Namenskonflikten hat das Projekt Vorrang.

## Best Practices für Subagents
- **Glasklare Ziele**: Eine Aufgabe, klar definierte Outputs (Markdown-Report, JSON o. ä.)
- **Determinismus erhöhen**: Formatvorgaben, Schrittpläne, Abbruchkriterien
- **Tool-Scope minimieren**: Nur benötigte Tools freischalten
- **Qualitätssicherung**: Subagent-Ergebnisse von einem zweiten Subagent (Reviewer) oder in CI validieren

## Beispiele (Accessibility)
- `accessibility-reporter`: Fuehrt Lighthouse/WCAG-Checks aus, erstellt Report in `accessibility-reporter.md`.
- `accessibility-fixer`: Liest Reports, implementiert Code-Fixes, ergänzt Tests, dokumentiert Änderungen in `accessibility-fixer.md`.

## Integration ins Team
- Projekt-Subagents im Repo halten und PR-Reviews einführen
- Onboarding: Kurzanleitung in der README, inklusive „Wie rufe ich Subagents auf?“
- CI: Subagents für wiederkehrende QA-Schritte (z. B. Accessibility, Lint, Security)

## Troubleshooting
- Subagent wird nicht gefunden: Namen prüfen, Speicherort korrekt? Sitzung neu starten.
- Fehlende Tools: In der Agent-Konfiguration explizit freischalten.
- Zu vage Ergebnisse: Systemprompt schärfen, Output-Format definieren, Beispiele geben.

