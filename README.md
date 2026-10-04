# JiCo for Jira & Confluence — MCP server for Jira Data Center

**Use Claude with Jira Data Center without handing personal data to the AI model.** JiCo is a local MCP server
that sits between your AI client (Claude Desktop, Claude Code, GitHub Copilot in VS Code) and your Jira Data Center.
It redacts personal data before the model sees it and holds every write action for a human approval.

> This repository is a **listing for MCP directories**. It contains no source code. JiCo is commercial software,
> installed as a signed package for macOS (Apple Silicon) or Windows (64-bit). Website: <https://getjico.com>

## What JiCo does

- **Redaction before the AI model.** Assignee, reporter, comment authors, mentions, check-digit numbers such as an
  IBAN, and secrets become placeholders such as «Person 1» before the model sees them. Free text is checked
  statistically — that finds a lot, but not everything.
- **Approval for every write action.** When the AI wants to change, comment on or create a ticket, JiCo stops and
  shows in plain language what is about to happen. It runs only after approval — and only if the ticket has not
  changed since.
- **Evidence.** What went to the AI model and who approved what is kept in an append-only log.

## MCP tools (Jira)

| Tool | Kind |
|---|---|
| `jira_ticket_lesen` · `jira_historie_lesen` · `jira_zeitbuchungen_lesen` | read (redacted) |
| `jira_suchen` · `jira_zaehlen` · `jira_aehnliche_suchen` · `jira_felder` · `jira_versionen` | read (redacted) |
| `jira_kommentar_schreiben` · `jira_kommentar_loeschen` · `jira_zeitbuchung_kommentar_leeren` · `jira_anhang_loeschen` | write — held for approval |
| `jira_status_wechseln` · `jira_ticket_verschieben` · `jira_ticket_anlegen` · `jira_feld_setzen` | write — held for approval |
| `jira_link_anlegen` · `jira_link_loeschen` | write — held for approval |
| `jico_selbstauskunft` · `jico_bestand` · `jico_konventionen` · `jico_freigaben_offen` | information about JiCo itself |

Unknown tools are treated as write tools (fail-closed).

## Getting started

1. Register in the [customer portal](https://portal.getjico.com/registrieren) — you receive a seven-day trial licence.
2. Install the package for your system.
3. Enter your Jira Data Center address and a personal access token (PAT).
4. In the Approval Cockpit, click *Set up automatically* for Claude Desktop or Claude Code.

Step by step: <https://getjico.com/en/jira-data-center-with-claude/>

## Limits

- Works with Jira **Data Center** today; Jira Cloud is not connected yet.
- No detection finds every piece of personal data in free text.
- JiCo protects what runs through JiCo. A second, unprotected Jira connection next to it bypasses it.

## Deutsch

JiCo ist ein lokaler MCP-Server für Jira Data Center: Personendaten werden geschwärzt, bevor das KI-Modell sie sieht,
und jede Schreibaktion wartet auf eine menschliche Freigabe. Anleitung:
<https://getjico.com/jira-data-center-mit-claude/>

## Contact

[support@getjico.com](mailto:support@getjico.com) · Provider: Dr. Kirchhof Ventures GmbH, Düsseldorf
([imprint](https://getjico.com/en/imprint/))
