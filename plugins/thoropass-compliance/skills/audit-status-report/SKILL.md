---
name: audit-status-report
description: >
  This skill should be used when the user asks for an "audit status report",
  "weekly compliance update", "how is the audit going", "audit progress",
  "summarize our SOC 2 audit", or wants a shareable summary of where a
  Thoropass audit stands.
metadata:
  version: "0.1.0"
---

# Audit Status Report

Write a concise, shareable status report for a Thoropass audit.

## Workflow

1. Call `list_audits`. If several are active, ask which one (or offer one report covering each).
2. Call `get_audit` for framework, audit window, dates and stage.
3. Call `get_audit_progress` for ER counts by status and percentage complete.
4. Call `list_evidence_requests` to find overdue and rejected ERs and upcoming due dates (next 14 days).
5. Call `list_monitors` and note any monitors that are failing or marked urgent, since these can create audit exceptions.
6. Optionally call `get_audit_scope` when the user asks which systems are in scope.

## Report format

Write in plain prose with a small table, suitable for pasting into Slack or email:

- **Headline**: one sentence — percent complete, on track / at risk, and why.
- **Progress**: table of ER counts by status.
- **Risks**: overdue ERs, rejected ERs, failing monitors (name + one-line impact).
- **Next 2 weeks**: ERs due, with owners.
- **Asks**: specific people or decisions needed.

Keep it under ~300 words unless the user asks for more detail. Call the audit "at risk" only when there are overdue or rejected ERs, or failing urgent monitors; otherwise "on track".

## Guardrails

- Read-only skill: do not modify any ERs, comments or attachments.
- Report numbers exactly as returned; do not estimate missing values.
