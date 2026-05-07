# SOP-004: Documenting a Dead End

> **Source:** Extracted from [Knowledge Architecture](../00_system_design/02_knowledge_architecture.md), Section 9  
> **Inspired by:** [NASA Lessons Learned Information System](../00_system_design/06_reference_reading.md#5-nasa-lessons-learned-information-system) — a 2012 NASA audit found 8/10 centres non-compliant with voluntary lessons-learned policies. That's why FORGE makes this **mandatory**.  
> **Trigger:** An experiment report confirms a hypothesis is refuted, or a line of inquiry is abandoned  
> **Owner:** Assigned researcher, reviewed by supervisor

---

## Critical Rule

> **A dead end entry is MANDATORY before any approach is officially abandoned.**  
> No approach may be declared "we already tried that" without a DE entry to prove it.

## Steps

1. Write DE entry using the template at `knowledge-commons/dead-end-registry/_TEMPLATE_dead_end.md`
2. Submit via Pull Request with the related Experiment Report attached
3. Supervisor reviews and confirms the root cause analysis is reasonable
4. DE is merged and becomes searchable in the registry
5. If the dead end was significant, present a **5-minute summary** at the next monthly review (SOP-005)

## Quality Checklist

Before submitting a DE entry, verify:

- [ ] "What Was Tried" is specific enough that someone else could replicate the attempt
- [ ] "Why It Failed" includes a root cause marked as [CONFIRMED] or [HYPOTHESIS]
- [ ] "Conditions That Might Change This" is honest — if conditions are genuinely different, the approach may be revisited
- [ ] "What We Learned" extracts positive knowledge, not just "it didn't work"
- [ ] Related Experiment Report is linked

## Why This Matters

Dead-end documentation is the most neglected and most valuable knowledge type. It prevents:
- Repeating failed approaches (wasting months of student time)
- Knowledge loss when researchers leave
- The "we already tried that" claim without evidence
