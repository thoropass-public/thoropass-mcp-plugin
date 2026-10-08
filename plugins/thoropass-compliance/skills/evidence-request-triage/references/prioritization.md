# ER Prioritization Rules

Rank open evidence requests in this order:

1. **Rejected / returned by auditor** — the auditor is waiting; feedback is in the comments.
2. **Overdue** — due date in the past. Sort by most overdue first.
3. **Due within 7 days.**
4. **Partial scope coverage** — some in-scope systems have evidence, others don't. Usually quick to finish.
5. **No owner assigned** — flag so someone picks it up.
6. **Everything else**, sorted by due date ascending.

Tie-breakers: ERs linked to more controls/requirements rank higher; ERs with zero attachments rank higher than ones with some.

## Suggested next-step wording

- Rejected: "Address auditor feedback: <one-line summary of comment>."
- Missing scope: "Add evidence for: <system names>."
- Policy-type requirement with no attachment: "Check for a published policy to attach (policy-evidence-matcher)."
- No owner: "Assign an owner."
- Ready but not submitted: "Review and submit."
