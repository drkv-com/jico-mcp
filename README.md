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

## Tools

Read tools return redacted data. Write tools are never executed directly: JiCo holds them as a proposal until a
human approves. Unknown tools are treated as write tools (fail-closed).

- `jira_ticket_lesen` — read a ticket: summary, description, links, comments (redacted)
- `jira_historie_lesen` — read the change history of a ticket (redacted)
- `jira_zeitbuchungen_lesen` — read the worklogs of a ticket (redacted)
- `jira_suchen` — search Jira with JQL
- `jira_zaehlen` — count JQL results grouped by a field
- `jira_aehnliche_suchen` — find similar tickets (duplicates, earlier cases)
- `jira_felder` — look up field definitions before using them in JQL
- `jira_versionen` — read the versions of a project
- `jira_kommentar_schreiben` — propose a comment (held for approval)
- `jira_kommentar_loeschen` — propose deleting a comment (held for approval)
- `jira_zeitbuchung_kommentar_leeren` — propose clearing a worklog comment (held for approval)
- `jira_anhang_loeschen` — propose deleting an attachment (held for approval)
- `jira_status_wechseln` — propose a workflow transition (held for approval)
- `jira_ticket_verschieben` — propose moving a ticket to another project (held for approval)
- `jira_ticket_anlegen` — propose a new ticket (held for approval)
- `jira_feld_setzen` — propose setting a field (held for approval)
- `jira_link_anlegen` — propose linking two tickets (held for approval)
- `jira_link_loeschen` — propose removing a link (held for approval)
- `jico_selbstauskunft` — how JiCo handles personal data
- `jico_bestand` — what is stored locally and how fresh it is
- `jico_konventionen` — the house conventions to follow before proposing a change
- `jico_freigaben_offen` — proposals waiting for approval

## Configuration

JiCo writes this entry for you: in the Approval Cockpit, *Settings › Connect to AI client › Set up automatically*.
For reference, the Claude Desktop entry on macOS (`claude_desktop_config.json`; on Windows JiCo inserts its own program path) — JiCo must be installed and running:

```json
{
  "mcpServers": {
    "jico": {
      "command": "/usr/local/bin/jico",
      "args": ["bruecke"]
    }
  }
}
```

Claude Code and GitHub Copilot in VS Code connect over HTTPS to the running JiCo; `jico einbinden` prints the
ready-made entry with the local address and access token.

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
