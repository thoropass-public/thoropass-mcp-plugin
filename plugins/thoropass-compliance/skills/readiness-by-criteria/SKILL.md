---
name: readiness-by-criteria
description: >
  This skill should be used when the user asks "how ready are we for SOC 2",
  "readiness by criteria", "which CC sections are behind", "progress by
  trust services criteria", "how are we doing on CC6", "which requirements
  are still open", or wants audit progress grouped by framework criteria
  instead of by individual evidence request.
metadata:
  version: "0.1.0"
---

# Readiness by Criteria

Show audit readiness grouped by framework criteria (for example SOC 2 CC1–CC9, or ISO 27001 clauses), so the user sees which areas of the framework are ready and which are behind.

## Workflow

1. Call `list_audits`. If more than one audit is active, ask which one.
2. Call `list_requirements` with the `audit_id`. It returns every requirement in one call, each with its `status` (open, under_review, completed, n/a), `citations` (criteria such as CC6.1), linked `evidence_requests` (with status) and mapped `controls`. Page through all results.
   - If the user asks about one area, pass `citation` (e.g. `CC6.1`) or `framework` to narrow the list.
3. Group requirements by criteria family using the citation prefix (e.g. CC6.1, CC6.2 → CC6). A requirement with several citations counts in each family it cites.
4. For each family, count requirements by status and compute percent completed (exclude `n/a` from the total).
5. Optionally call `list_global_controls` with the `audit_id` to add control health (`implementation_status`: healthy, flagged, in_progress, not_started, no_health). Call out any `flagged` controls in families that are behind.

## Response format

- **Headline**: overall percent of requirements completed and the 2–3 families furthest behind.
- **Table**: Criteria family, Requirements, Completed, Under review, Open, % complete. Sort with the least complete first.
- **Focus areas**: for the least complete families, list the open requirements and their open evidence requests (display_id, name, status).
- Offer to run evidence-request-triage on the open ERs in a family.

## Guardrails

- Read-only skill: do not change requirements, ERs or controls.
- Report counts exactly as returned; do not estimate.
- If `list_requirements` returns nothing, say the audit has no requirements loaded yet rather than reporting 0% readiness.
