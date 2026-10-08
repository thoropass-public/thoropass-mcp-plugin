---
name: audit-explainer
description: >
  This skill should be used when the user asks "where are we in the audit",
  "what happens next in our audit", "explain our audit", "what does this
  audit status mean", "how does a Thoropass audit work", "what do I need to
  do before fieldwork", or is new to compliance audits and wants a
  plain-language explanation of where a Thoropass audit stands and what
  comes next.
metadata:
  version: "0.1.0"
---

# Audit Explainer

Explain, in plain language, where a Thoropass audit is in its lifecycle, what the numbers mean, and what the customer needs to do next. Write for someone who has never been through an audit. For a shareable status report for people who already know the process, use the audit-status-report skill instead.

## Workflow

1. Call `list_audits`. If more than one audit is active, ask which one. If only one is active, use it and say so.
2. Call `get_audit` for the framework, audit window and dates.
3. Call `get_audit_progress`. Use `current_status`, `days_to_deadline`, `review_end_date`, `er_counts`, `completion_percentage`, `pace`, `returned_by_auditor` and `awaiting_customer_reply`.
4. Explain the stage using `current_status`:

   | `current_status` | Plain-language meaning |
   |------------------|------------------------|
   | `requested` | The audit has been requested and is being set up. |
   | `initiated` | The audit is set up. The team is preparing: agreeing the engagement letter and the scope before fieldwork. |
   | `fieldwork` | The auditor is actively testing. This is when evidence requests are uploaded, reviewed and sometimes returned for changes. |
   | `draftReport` | Testing is done. The auditor is writing the report; the customer may be asked to review a draft. |
   | `completed` | The audit is finished and the report is issued. |

   If `current_status` is null, say the stage is not set yet rather than guessing.

5. Explain evidence request (ER) statuses using `er_counts`:
   - `not_yet_open`: requested later in the audit; nothing to do yet.
   - `not_started`: open, but no one has started it.
   - `in_progress`: someone is working on it or the auditor is reviewing it.
   - `completed`: accepted by the auditor.

6. Explain pace: if `pace.at_risk` is true, say the team is completing about `pace.actual_per_week` ERs per week but needs about `pace.required_per_week` to finish by the deadline.

## Response format

- **Where you are**: one or two sentences naming the stage and what it means.
- **How far along**: `completion_percentage`, the ER status counts in a small table, and days to the deadline.
- **What happens next**: the next stage and what typically triggers it.
- **What you need to do now**: up to 3 concrete actions, taken from `returned_by_auditor`, `awaiting_customer_reply`, `overdue` and `due_soon`, in that order.
- **Glossary** (only if the user seems new): ER, auditor, fieldwork, audit window.

Keep it under ~300 words unless the user asks for more.

## Guardrails

- Read-only skill: do not change ERs, comments or attachments.
- Report numbers exactly as returned; do not estimate missing values.
- Do not promise dates or outcomes the data does not show.
