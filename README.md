<h1 align="center">
  <img src="nla-team.png" alt="NLA Team logo" width="160">
  <br>
  NLA Team
</h1>

<p align="center"><strong>Your next engineering team is a team of agents.</strong><br>Agile Teams · MCP · RAG · Multi-model Orchestration</p>

> **Give the team a goal. Follow the work. Review the result.**

**Status: experimental · private testing · source code is not open source at this time.**

This repository contains an architecture preview, not the implementation or an installable release.

## One goal. A coordinated team.

Persistent AI employees built on [Next Level Agent](https://github.com/pickleshell/next-level-agent).

```mermaid
flowchart TB
    Owner["You<br/>Goal · Priorities · Acceptance"] --> Lead["Team Lead<br/>Plan · Delegate · Integrate"]
    Lead --> Architect["Architect"]
    Lead --> Developer["Developer"]
    Lead --> Reviewer["Independent Reviewer"]
    Architect <--> Core["Team Core<br/>ACP messages · Durable state"]
    Developer <--> Core
    Reviewer <--> Core
    Lead <--> Core
    Core --> Memory[("RAG-style memory<br/>Private · Curated project knowledge")]
    Core --> Lab["NLA Lab<br/>Conversations · Summaries · Status"]
    Architect --> MCP["MCP servers<br/>Connected tools & services"]
    Developer --> MCP
    Reviewer --> MCP
    Lab --> Owner
```

**MCP connects tools. ACP connects teammates.** Native tools and APIs remain supported.

| Concept | Purpose |
| --- | --- |
| **Agile Teams** | Clear ownership · Parallel work · Feedback |
| **Scrum / Kanban** | Backlog · Ready/Done criteria · Review |
| **Model Orchestras** | Specialist roles and model selection within each employee |
| **RAG-style memory** | Retrieve reviewed knowledge · Preserve provenance |
| **Persistent state** | Checkpoints · Session recovery · Continuity |
| **Independent review** | Exact artifacts · Reproducible checks · Honest results |

## Agent → Team → Lab

**One employee is already an agent system.** Each NLA instance can orchestrate specialist roles, delegate work and review results. NLA Team coordinates these persistent employees; the Lab ecosystem adds observation and a developing cross-team management loop.

| Layer | Responsibility |
| --- | --- |
| **Next Level Agent** | Individual execution · Internal model orchestra · Context continuity |
| **NLA Team** | Team Lead · Persistent employees · ACP coordination · Independent review |
| **NLA Lab ecosystem** | Cross-team visibility · Evidence · Proposed autonomous process management |

### Conceptual organization

The following diagram expresses the **target vision**, not a list of shipped capabilities. “Supervisor” names the supervisory layer; its reasoning and enforcement responsibilities are separated in the operational design below.

```text
┌────────────────────────────────────────────────────────────────────────┐
│                                NLA Lab                                 │
│                                                                        │
│  ┌──────────────────────────────────────────────────────────────────┐  │
│  │                            SUPERVISOR                            │  │
│  │   • State & Ledger Tracker      • Risk Interceptor & Sandbox     │  │
│  │   • Token/Budget Policy Manager • Global Health & Anti-Loop      │  │
│  └─────────────────────────────────┬────────────────────────────────┘  │
│                                    │                                   │
│                       (Event Bus / RPC Control Channel)                 │
│          ┌─────────────────────────┴────────────────────────┐          │
│          ▼                                                  ▼          │
│   ┌──────────────┐                                   ┌──────────────┐  │
│   │   NLA Team   │                                   │   NLA Team   │  │
│   │ ┌──────────┐ │                                   │ ┌──────────┐ │  │
│   │ │  NLA #1  │ │                                   │ │  NLA #1  │ │  │
│   │ └──────────┘ │                                   │ └──────────┘ │  │
│   │ ┌──────────┐ │                                   │ ┌──────────┐ │  │
│   │ │  NLA #2  │ │                                   │ │  NLA #2  │ │  │
│   │ └──────────┘ │                                   │ └──────────┘ │  │
│   └──────────────┘                                   └──────────────┘  │
└────────────────────────────────────────────────────────────────────────┘
```

### Operational boundaries

**Lab observes. Manager reasons. Controller and Gateway enforce. Leads coordinate delivery.**

```text
             User: goals, authority, escalated decisions
                                │
                     Autonomy Controller
              Schedule · Journal · Budgets · No overlap
                                │
                          NLA Manager
                 Assess progress · Resolve blockers
                         │              ▲
                  Control Gateway       │ Read-only MCP
                         │           NLA Lab
                         ▼       State · History · Evidence
                      Team Lead
                         │
                 ┌───────┼───────┐
                 ▼       ▼       ▼
                NLA     NLA     NLA
               Build   Test    Independent review
                 │
          Internal model orchestra
```

The management loop is being implemented and validated. The existing **Lab MCP remains read-only**; coordination actions use a separate scoped gateway. Team Core remains authoritative for team records.

- **Evidence before intervention:** freshness, provenance and incomplete observations remain visible.
- **Lead-owned execution:** Manager coordinates enrolled teams through their Leads.
- **Bounded autonomy:** scoped actions, durable obligations and explicit escalation.
- **No blind replacement:** an invocation with an unknown outcome blocks replacement until reconciliation.

A journal is **not** automatic rollback of files or external effects. Dynamic team resizing, universal risk interception and guaranteed anti-loop recovery are not claimed as implemented. Reliable cancellation/quiescence and confirmed external operator notification remain release gates for unattended operation.

The objective is measurable: **less operator prompting, verified recovery from stalled work, and completed tasks backed by evidence.** Architectural scope alone is not proof of superiority over another framework.

## Several groups. One outcome.

Illustrative workflow: **build an internal knowledge portal**.

```mermaid
flowchart LR
    Goal["Product goal"] --> Architecture["Architecture group<br/>Interfaces & acceptance"]
    Architecture --> Backend["Service team<br/>Search & APIs"]
    Architecture --> Frontend["Experience team<br/>UI & workflows"]
    Backend <--> Frontend
    Backend --> QA["Quality group<br/>Independent review"]
    Frontend --> QA
    QA -->|Corrections| Backend
    QA -->|Corrections| Frontend
    QA --> Delivery["Integration<br/>Evidence & handover"]
    Delivery --> Owner["Owner acceptance"]
```

Organizational patterns, not a claim of automatic Scrum ceremonies or a cross-team dispatcher.

## Testing: progress and limits

**Observed in private testing:** durable messaging, shared-memory promotion, versioned handoffs, independent review, and session recovery.

**43 employees · 13 teams** updated and restarted in one maintenance run, with prior sessions restored and infrastructure checks passing. This is operational evidence, not a productivity benchmark.

**Still improving:** stalled handoffs · interface drift · model reliability · context recovery · coordination cost.

Human oversight remains necessary. Healthy processes do not prove completed work. Current deployments assume trusted environments.

## Interested?

**Private testers · Architecture reviewers · Integration partners**

Have a workflow worth testing? Want to collaborate or ask a question? [Open an issue](https://github.com/pickleshell/nla-team/issues) if you have repository access, or visit the [maintainer’s GitHub profile](https://github.com/pickleshell).

Testing access is arranged individually. **Implementation source remains private; no public release date is promised.**

---

Built around [Next Level Agent](https://github.com/pickleshell/next-level-agent). See that project for its release status, acknowledgements and licensing. This preview does not publish the private NLA Team implementation.
