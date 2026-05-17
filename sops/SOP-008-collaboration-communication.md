# SOP-008: Collaboration Communication

> **Source:** [Collaboration Protocol](../00_system_design/04_collaboration_protocol.md)  
> **Trigger:** All ongoing collaboration activities  
> **Owner:** Research Lead — responsible for maintaining meeting cadence

---

## Meeting Schedule

| Meeting | When | Duration | Attendees | Purpose |
|---------|------|----------|-----------|---------|
| **Weekly Standup** | Monday | 30 min | Students + Research Lead | Progress, blockers, week plan |
| **Technical Sync** | Bi-weekly (Tue) | 60 min | All researchers + supervisors | Deep technical review |
| **Steering Committee** | Monthly (Last Fri) | 90–120 min | All stakeholders | Portfolio review, gate decisions |
| **Radar Review** | Quarterly | 60 min | Research Lead + track owners | Technology Radar update |

> **Timezone rule:** All times shared in UTC with local conversions. If timezone conflict, standup moves to async (GitHub Discussion).

---

## Async Communication

| Channel | Use For | Response SLA |
|---------|---------|-------------|
| **GitHub Pull Requests** | Document/code reviews | 48 hours |
| **GitHub Discussions** | Decisions, open questions, async standups | 24 hours |
| **GitHub Issues** | Bugs, feature requests, experiment backlog | 72 hours |
| **Slack/Teams** | Quick questions, informal discussion | Same day |
| **Email** | Formal university communications | 48 hours |

---

## Decision Logging

1. All decisions captured in GitHub Discussions (tagged `decision`)
2. Format: **Decision + Rationale + Who + Date**
3. Significant decisions also captured in monthly report and/or ADR
4. **Rule:** If it's not in writing, it didn't happen

---

## Meeting Agenda Template

```markdown
# [Meeting Type] — [YYYY-MM-DD]

**Attendees:** [Names]  
**Facilitator:** [Name]

## Agenda
1. [Item 1] — [Owner] — [Time]
2. [Item 2] — [Owner] — [Time]

## Notes
- [Key discussion points]

## Decisions Made
- [Decision]: [Rationale] — Decided by [Names]

## Action Items
- [ ] [Owner]: [Action] — due [date]
```

---

## Escalation Quick Reference

| Situation | Escalate To | Timeline |
|-----------|-------------|----------|
| Student stuck > 1 week | Academic supervisor | 5 days |
| Equipment/lab blocked | Hardware Team + Research Lead | 48 hours |
| IP concern | Research Lead immediately | Same day |
| Methodology disagreement | Steering Committee | Next meeting |

---

*Review quarterly. Update when communication tools or team composition changes.*
