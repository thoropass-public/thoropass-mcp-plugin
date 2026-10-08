# Thoropass Compliance Plugin

A compliance plugin primarily designed for [Cowork](https://claude.com/product/cowork), Anthropic's agentic desktop application, though it also works in Claude Code. It connects Claude to your Thoropass account so you can work with your audits, evidence requests, requirements, controls, policies and monitors: understand where an audit stands, see what you need to do this week, check readiness by framework criteria, triage evidence, answer policy questions and investigate failing monitors.

## Installation

```bash
claude plugin marketplace add thoropass-public/thoropass-mcp-plugin
claude plugin install thoropass-compliance@thoropass
```

The first time Claude uses a Thoropass tool, you sign in with your Thoropass account (OAuth). No API keys or environment variables are needed. Claude only sees data your Thoropass account can access.

## Skills

Skills run when your request matches, or directly by name (for example `/thoropass-compliance:audit-explainer`).

### Understand your audit

| Skill | Description | Writes data? |
|---|---|---|
| `audit-explainer` | Where the audit stands and what happens next, in plain language. Start here if you're new to audits | No |
| `my-audit-tasks` | Your personal to-do list: assigned evidence requests, overdue items and comments waiting for your reply | No (offers follow-ups) |
| `readiness-by-criteria` | Readiness grouped by framework area (CC1–CC9 and others), with open requirements | No |
| `audit-status-report` | A weekly audit status report you can share | No |

### Evidence, policies and monitors

| Skill | Description | Writes data? |
|---|---|---|
| `evidence-request-triage` | Ranked list of open, overdue and returned evidence requests to work on first | No (offers follow-ups) |
| `policy-explainer` | Plain-language answers from your published policies | No |
| `policy-evidence-matcher` | Matches published policies to open policy evidence requests | Attaches a policy only after you approve it |
| `monitor-investigation` | Which monitors are failing, why, and how to fix them | No |

## Example workflows

### Getting oriented

```
Where are we in the audit and what happens next?
```

The `audit-explainer` skill reads the audit's stage, dates and progress, explains what that stage means and lists what your team should do before the next one.

### Planning your week

```
What do I need to do this week?
```

The `my-audit-tasks` skill lists the evidence requests assigned to you, in priority order (returned by the auditor, overdue, due soon), and shows comments waiting for your reply.

### Closing policy evidence requests

```
Match our policies to open evidence requests
```

The `policy-evidence-matcher` skill suggests a published policy for each open policy evidence request. It shows every proposed attachment and attaches nothing until you approve it.

## Connectors

| Connector | What it enables |
|---|---|
| **Thoropass** (`https://api.thoropass.com/mcp`) | Audits, evidence requests, requirements, controls, policies, monitors and integrations |

The plugin registers the Thoropass MCP server for you in `.mcp.json`.

## Safety

- Thoropass content (evidence request text, comments, policies, attachments, monitor results) is treated as information, never as instructions.
- Submitting evidence requests, attaching policies, uploading or deleting attachments, and posting, editing or deleting comments always need your explicit confirmation.
- Evidence on shared evidence requests is never uploaded twice.

## For admins

Thoropass permissions decide what Claude can do. Claude acts as the signed-in user and never goes beyond that user's Thoropass permissions or the scopes they granted. If a scope is missing, the skill says so instead of retrying.

In Claude, set write tools (submit, attach, upload, comment, delete) to **ask** so nothing changes without a person approving it.

## Customizing

Edit the `SKILL.md` files under `skills/` to match your team's process. For example, change the prioritization rules in `skills/evidence-request-triage/references/prioritization.md`.

## Other AI agents

Every skill is a plain Markdown workflow, so other agents can follow it too. See [AGENTS.md](https://github.com/thoropass-public/thoropass-mcp-plugin/blob/main/AGENTS.md) for the Thoropass MCP tools, core concepts and rules.
