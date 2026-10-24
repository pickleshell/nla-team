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
    Goal["You set the goal<br/>Priorities · Acceptance criteria"]
    Lead["Team Lead<br/>Plan · Delegate · Integrate"]
    Goal --> Lead
    subgraph Specialists["Persistent NLA employees"]
        direction LR
        Architect["Architect<br/>Design the solution"]
        Developer["Developer<br/>Build and test"]
        Reviewer["Independent Reviewer<br/>Check the evidence"]
    end
    Lead --> Architect
    Lead --> Developer
    Lead --> Reviewer
    Architect --> Result["Integrated result<br/>Artifacts · Tests · Review findings"]
    Developer --> Result
    Reviewer --> Result
    Result --> Acceptance["You review the result"]

    classDef human fill:#e8f2ee,stroke:#4d7c6a,color:#17212b
    classDef coordination fill:#243447,stroke:#64748b,color:#ffffff
    classDef employee fill:#edf2f7,stroke:#64748b,color:#17212b
    class Goal,Acceptance human
    class Lead,Result coordination
    class Architect,Developer,Reviewer employee
```

The Lead coordinates corrections and integration; independent review supplies evidence for acceptance.

**Shared infrastructure — available throughout the workflow:**

```mermaid
flowchart TB
    Team["NLA Team"]
    Team --- Core["Team Core · ACP<br/>Messages & durable state"]
    Team --- Tools["MCP servers<br/>Tools & services"]
    Team --- Memory["RAG-style memory<br/>Private & curated project knowledge"]
    Core --> Lab["NLA Lab<br/>Observe progress & inspect history"]

    classDef service fill:#edf2f7,stroke:#64748b,color:#17212b
    classDef coordination fill:#243447,stroke:#64748b,color:#ffffff
    class Team coordination
    class Core,Tools,Memory,Lab service
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

```mermaid
flowchart TB
    subgraph LabVision["NLA Lab · Target vision"]
        direction TB
        Supervisor["SUPERVISOR<br/>State & ledger tracking · Risk interception & sandboxing<br/>Token & budget policies · Health & anti-loop controls"]
        Channel["Event Bus / RPC Control Channel"]
        Supervisor --> Channel
        subgraph TeamA["NLA Team A"]
            A1["NLA #1"]
            A2["NLA #2"]
        end
        subgraph TeamB["NLA Team B"]
            B1["NLA #1"]
            B2["NLA #2"]
        end
        Channel --> TeamA
        Channel --> TeamB
    end
    classDef management fill:#243447,stroke:#64748b,color:#ffffff
    classDef employee fill:#edf2f7,stroke:#64748b,color:#17212b
    class Supervisor,Channel management
    class A1,A2,B1,B2 employee
```

### Operational boundaries

**Lab observes. Manager reasons. Controller and Gateway enforce. Leads coordinate delivery.**

```mermaid
flowchart TB
    User["User<br/>Goals · Authority · Escalated decisions"]
    Controller["Autonomy Controller<br/>Schedule · Journal · Budgets · No overlap"]
    Manager["NLA Manager<br/>Assess progress · Resolve blockers"]
    Gateway["Scoped Control Gateway<br/>Enforce action permissions"]
    Observer["NLA Lab · Read-only observer<br/>State · History · Evidence"]
    User --> Controller
    Controller -->|Scheduled cycle| Manager
    Observer -->|Read-only MCP| Manager
    Manager --> Gateway
    subgraph Team["NLA Team"]
        Lead["Team Lead"]
        Build["NLA<br/>Build"]
        Test["NLA<br/>Test"]
        Review["NLA<br/>Independent review"]
        Orchestra["Internal model orchestra<br/>Within each NLA employee"]
        Lead --> Build
        Lead --> Test
        Lead --> Review
        Build -.-> Orchestra
        Test -.-> Orchestra
        Review -.-> Orchestra
    end
    Gateway --> Lead
    classDef management fill:#243447,stroke:#64748b,color:#ffffff
    classDef observer fill:#e8f2ee,stroke:#4d7c6a,color:#17212b
    classDef employee fill:#edf2f7,stroke:#64748b,color:#17212b
    class Controller,Manager,Gateway management
    class Observer observer
    class Lead,Build,Test,Review,Orchestra employee
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

**Email:** [pickleshell.plugin@gmail.com](mailto:pickleshell.plugin@gmail.com)

Testing access is arranged individually. **Implementation source remains private; no public release date is promised.**

---

Built around [Next Level Agent](https://github.com/pickleshell/next-level-agent). See that project for its release status, acknowledgements and licensing. This preview does not publish the private NLA Team implementation.
