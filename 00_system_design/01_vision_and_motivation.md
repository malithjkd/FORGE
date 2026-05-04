# FORGE: Vision and Motivation

> **Document Status:** Founding Vision Document  
> **Author:** Malith Jayawardhana (MJ)  
> **Date:** 2026-05-04  
> **Purpose:** Captures the original thinking behind why PBA needs a research management system, not just a project plan

---

## 1. Context

We are collaborating with the University of Moratuwa (UoM), Sri Lanka, to undertake two master's research projects as part of building a three-person internal development team. Each project runs for 12 months. Under our agreement, PBA provides the initial guidance — the problem statement, available facilities and resources, and our expected deliverables. The university selects two master's students, each assigned a three-person mentoring panel. The students then conduct their own literature reviews and select suitable research paths to achieve our goals.

I (MJ) am the one who presented this idea to upper management, secured the funding, and am managing the project from the PBA side. My role includes guiding the teams periodically, monitoring progress, and coordinating between the university and our company.

---

## 2. The Original Plan

The initial plan was straightforward:

1. Give students access to the experimental setup.
2. Ask them to develop a data collection method and run tests to identify several failure types.
3. Identify failure types that can be classified based on the collected data, then develop ML models to detect them.
4. Predict the Remaining Useful Life (RUL).
5. Deliver a working prototype.
6. Begin working with customers.

---

## 3. Shortcomings of the Original Plan

That plan has several critical shortcomings:

1. **Single point of failure** — The plan is susceptible to single points of failure at every stage.
2. **No room for change** — There is no mechanism to adopt new ideas or pivot when circumstances change.
3. **Failure is not accounted for** — The plan assumes linear success; there is no provision for what happens when an approach fails.

---

## 4. A Better Approach: Building a System, Not Just a Project

Instead of following the original linear plan, I began thinking about an alternative method for managing the project — one built around a **system** rather than a single path:

1. We need to explore alternative approaches to managing the project.
2. The approach must not rely on a single champion person, a single idea, or a single process.
3. It must allow for failure and the adoption of new ideas.
4. It should achieve the business goal of developing customer-facing predictive maintenance software and hardware tools — but as a **byproduct** of the system, not as its sole purpose.
5. It should keep developing new ideas and new products — generating more useful outcomes than a single customer-facing tool.
6. It must learn from failures, document the full development journey, and track both the paths we have explored and those we have yet to explore.
7. The system should work **by itself** rather than working toward a single fixed goal.

---

## 5. Why We Need Such a System

1. **Reduce single points of failure** — Ensure that the failure of one person, one system, or one direction does not determine the project's success.
2. **Increase flexibility** — Allow the system to adapt to change.
3. **Increase development speed** — Establish a continuous process rather than a stop-start cycle.
4. **Increase product quality** — Accumulated knowledge leads to better outputs.
5. **Increase innovativeness** — Parallel exploration encourages novel solutions.
6. **Increase sustainability** — The system persists beyond any individual contributor.
7. **Learn from both failures and successes** — Document successful paths and their learnings alongside failed paths and their outcomes. This prevents repeating failures and allows us to build on proven knowledge.
8. **Create a competitive moat** — If we work on a single product or a single achievement, it can be easily replicated by the competition. By creating a system, we make it difficult for competitors to replicate our success. They might figure out the one product we developed, but they may not be able to figure out the system that produced it.
9. **Enable faster adaptation** — We can adopt and change technologies and ideas over time.
10. **Accept contributions from multiple sources** — Universities, research teams, research projects, internal teams, and even customers can all feed into the system.

---

## 6. What's Next

To make this vision real, we need to answer three questions:

1. **What does it take to develop such a system?**
2. **What are the key considerations?**
3. **How do we start?**

The answer to these questions is the **FORGE Knowledge Architecture** — see [02_knowledge_architecture.md](./02_knowledge_architecture.md).

---

*This document is the founding vision for FORGE. It captures the original thinking and motivation as they were conceived. The architectural details, templates, SOPs, and implementation roadmap are developed in the Knowledge Architecture document.*
