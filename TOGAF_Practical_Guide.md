# TOGAF Practical Guide

## Overview

The Open Group Architecture Framework (TOGAF) is a structured method for designing, planning, implementing, and governing enterprise architecture. Its heart is the Architecture Development Method (ADM), a repeatable cycle that helps architects align technology with business goals. This guide focuses on the essentials a new architect needs to put TOGAF into practice.

## Core Components at a Glance

- **Architecture Development Method (ADM)**: The step-by-step process for building and maintaining architectures.
- **Architecture Content Framework**: Defines the deliverables, artifacts, and building blocks produced in each ADM phase.
- **Enterprise Continuum and Repository**: Organizes reusable architecture assets, from generic reference models to organization-specific components.
- **Architecture Capability Framework**: Guidance on governance, skills, and processes required to run architecture as a function.

## Roles You Will Interact With

- **Business stakeholders**: Define strategic goals, operating models, and business capabilities.
- **IT leadership and product owners**: Own delivery roadmaps and platform decisions.
- **Solution and domain architects**: Translate enterprise-level direction into solution designs.
- **Portfolio and project managers**: Align initiatives with approved architecture roadmaps.
- **Governance boards**: Ensure compliance with principles, standards, and reference architectures.

## Getting Ready

1. Identify executive sponsors and confirm architecture charter or mandate.
2. Collect baseline information: business strategies, application inventory, data catalogs, infrastructure footprint.
3. Define architecture principles and decision criteria. Keep them short, actionable, and measurable.
	- Example: "Buy before build" – evaluate commercial solutions before custom development.
	- Example: "API-first" – every service exposes a documented interface for reuse.
	- Example: "Cloud-native" – new workloads must run on containerized, stateless platforms.
4. Choose tooling (spreadsheets, modeling tools, wiki) to manage artifacts and traceability.
	- **Low budget**: Confluence, draw.io, and shared spreadsheets.
	- **Medium budget**: Archi (free) or Sparx EA with SharePoint or Teams.
	- **Enterprise**: LeanIX, Ardoq, or BiZZdesign with integrated governance workflows.
5. Agree on cadence for governance checkpoints and stakeholder updates.

## Architecture Development Method (ADM)

Each ADM phase creates or updates specific artifacts. Phases are iterative; expect to revisit earlier work as new information emerges.

### Phase A: Architecture Vision
- **Purpose**: Establish scope, stakeholders, objectives, and the value proposition of the architecture effort.
- **Key Artifacts**: Vision document, stakeholder map, value case, approval plan.
- **Practical Example**: Launching a digital transformation program, capture a one-page story outlining target customer experience, supporting capabilities, and success metrics.

### Phase B: Business Architecture
- **Purpose**: Describe current and target business capabilities, processes, and organizational structures.
- **Key Artifacts**: Capability map, process heat map, value streams, org impacts.
- **Practical Example**: Map order-to-cash processes, identify manual handoffs, and propose a future state with automated credit checks and unified customer view.
- **Real Scenario**: A retailer finds refunds take 14 days because five teams re-enter data manually. Target state automates approvals, routes cases through a shared portal, and delivers refunds in three days.

### Phase C: Information Systems Architectures
- **Data Architecture**: Define data entities, ownership, and flows.
- **Application Architecture**: Outline applications, services, and their interactions.
- **Key Artifacts**: Data matrix, application portfolio catalog, integration diagrams.
- **Practical Example**: Document how customer data moves from CRM to billing to analytics, and propose a shared customer master service.

### Phase D: Technology Architecture
- **Purpose**: Specify infrastructure, platforms, and technology services required by applications and data.
- **Key Artifacts**: Platform reference models, infrastructure topology, technology standards.
- **Practical Example**: Select a hybrid cloud design with standardized container platforms, shared observability stack, and disaster recovery tiers.

### Phase E: Opportunities and Solutions
- **Purpose**: Identify solution building blocks, package work into projects or workstreams, and assess implementation options.
- **Key Artifacts**: Work packages, transition options, solution concept diagrams.
- **Practical Example**: Group initiatives into customer identity, order management, and analytics modernization workstreams with clear dependencies.

### Phase F: Migration Planning
- **Purpose**: Build the roadmap, prioritize projects, and align with budget cycles.
- **Key Artifacts**: Implementation roadmap, benefit and risk assessments, resource plans.
- **Practical Example**: Produce a four-quarter roadmap showing MVP launch, data foundation, and phased rollout of new channels.

### Phase G: Implementation Governance
- **Purpose**: Provide architecture oversight during delivery, ensure conformance with standards, and manage change requests.
- **Key Artifacts**: Architecture compliance assessments, design decision logs, waiver approvals.
- **Practical Example**: Run design reviews at sprint boundaries, document deviations, and track mitigation actions.

### Phase H: Architecture Change Management
- **Purpose**: Monitor business and technology changes, trigger new ADM cycles when needed, and retire outdated assets.
- **Key Artifacts**: Change requests, architecture backlog, updated principles or standards.
- **Practical Example**: Add a new cybersecurity regulation to the backlog, initiate a focused mini-cycle for data privacy enhancements.

### Requirements Management (continuous)
- **Purpose**: Capture and reconcile requirements across all phases.
- **Practice Tip**: Maintain a single backlog or register with status, owner, phase impact, and traceability to decisions.

## Applying TOGAF in Daily Work

- **Start small**: Pick a pilot scope (e.g., customer experience program) to demonstrate value before scaling.
- **Reuse building blocks**: Pull reference models, patterns, and standards from the repository before inventing new ones.
- **Engage stakeholders early**: Validate business outcomes and technical feasibility before locking roadmaps.
- **Measure outcomes**: Tie architecture decisions to KPIs such as customer satisfaction, cycle time reduction, or platform stability.
- **Document decisions**: Record rationale, alternatives, and impacts. Future architects will rely on these notes.

## Example Deliverable Set for a New Program

| Phase | Deliverable | Summary |
|-------|-------------|---------|
| A | Vision deck | One-page summary of why and what we are changing |
| B | Capability heat map | Highlights high-impact capabilities needing investment |
| C | Data flow diagram | Shows customer data lifecycle across systems |
| D | Technology standards list | Approved platforms, hosting patterns, and guardrails |
| E/F | Roadmap slide | Sequenced work packages with major milestones |
| G | Compliance checklist | Criteria used during solution design reviews |
| H | Architecture backlog | Ranked list of future enhancements and emerging requirements |

## Tips for Successful Adoption

1. Communicate architecture value in business terms, not framework jargon.
2. Keep artifacts lightweight; focus on clarity over exhaustive detail.
3. Align cadence with corporate planning cycles and funding gates.
4. Share early drafts for feedback, then baseline and control changes.
5. Pair with delivery teams to ensure architecture recommendations translate into backlog items.

## Typical Phase Durations (adjust for scope)

| Phase | Small Project | Medium Program | Large Transformation |
|-------|---------------|----------------|---------------------|
| A: Vision | 1-2 weeks | 2-4 weeks | 4-6 weeks |
| B: Business | 2-3 weeks | 4-6 weeks | 8-12 weeks |
| C: Information Systems | 2-3 weeks | 4-6 weeks | 8-10 weeks |
| D: Technology | 1-2 weeks | 3-4 weeks | 4-6 weeks |
| E/F: Solutions & Planning | 2-3 weeks | 4-6 weeks | 6-8 weeks |
| G: Implementation | Ongoing | Ongoing | Ongoing |
| H: Change Management | Continuous | Continuous | Continuous |

## Common Pitfalls to Avoid

- Analysis paralysis: documenting current state indefinitely without delivering improvements.
- Ivory tower designs: crafting target architectures that delivery teams cannot build.
- Stakeholder gaps: proceeding without executive sponsorship or business buy-in.
- Over-documentation: producing artifacts no one reads; keep them under 20 focused pages.
- Ignoring quick wins: deferring all value to long-term programs instead of shipping incremental benefits.

## Stakeholder Communication Template

**Executive summary format**

1. Current challenge (1-2 sentences describing the pain).
2. Proposed solution (bullets covering scope, approach, and boundaries).
3. Business benefits (quantified where possible).
4. Investment required (people, time, and budget estimates).
5. Key risks and mitigations (top three items with owners).
6. Immediate next steps (clear actions with accountable roles).

## Reference Models Worth Knowing

- TOGAF Foundation Architecture Technical Reference Model (TRM)
- TOGAF Integrated Information Infrastructure Reference Model (III-RM)
- Industry-specific reference architectures from standards bodies or cloud providers

## When to Consider a New ADM Cycle

- Major shifts in business strategy, mergers, or new market entry
- Significant technology changes (cloud migration, platform renewal)
- Regulatory or compliance mandates impacting processes or data
- Persistent architecture debt that blocks delivery timelines

## Maintaining the Architecture Repository

- Organize by domains (business, data, application, technology) and lifecycle (baseline, transition, target).
- Tag assets with owner, date, and applicability to avoid stale information.
- Archive deprecated artifacts but retain traceability for audit and lessons learned.

## Quick Self-Check for New Architects

- Can you explain the current and target business capabilities in plain language?
- Are your architecture principles actively guiding decisions?
- Do stakeholders understand the roadmap and its business outcomes?
- Is every roadmap item traceable to requirements and strategic objectives?
- Are governance decisions documented and accessible to delivery teams?

## Further Reading

- The TOGAF Standard, 10th Edition (The Open Group)
- The Open Group pocket guides on ADM and Architecture Content
- Enterprise Architecture as Strategy by Ross, Weill, and Robertson

Use this guide as a starting point. Adapt the depth and timing of each phase to fit your organization's culture, governance, and delivery practices while keeping the core TOGAF principles intact.