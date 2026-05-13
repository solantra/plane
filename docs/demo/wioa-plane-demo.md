# WIOA Assignments Plane Demo

This demo shows how to run WIOA assignment operations and supporting engineering work in Plane. It is designed for a 20 to 30 minute walkthrough using one workspace with two projects:

- `WIOA Assignments` for program operations, participant assignment work, eligibility checks, partner handoffs, and case follow-up.
- `Engineering Delivery` for product/data/integration work that supports the WIOA workflow.

## Demo Setup

Create a workspace named `Solantra Workforce Ops`.

Create these projects:

| Project              | Identifier | Purpose                                                                                |
| -------------------- | ---------- | -------------------------------------------------------------------------------------- |
| WIOA Assignments     | WIOA       | Operational tracking for participant assignments and follow-up                         |
| Engineering Delivery | ENG        | Engineering backlog for automation, reporting, integrations, and workflow improvements |

Create these labels:

| Label             | Use                                                              |
| ----------------- | ---------------------------------------------------------------- |
| `wioa`            | WIOA program work                                                |
| `eligibility`     | Eligibility verification                                         |
| `case-management` | Counselor or case manager follow-up                              |
| `partner-handoff` | Work involving external training providers or workforce partners |
| `reporting`       | Dashboards, exports, compliance reports                          |
| `automation`      | Workflow or notification automation                              |
| `data-quality`    | Missing, duplicate, or inconsistent data                         |
| `risk`            | Work with compliance, deadline, or participant-impact risk       |

Create these modules:

| Project              | Module                         | Demo purpose                                      |
| -------------------- | ------------------------------ | ------------------------------------------------- |
| WIOA Assignments     | Intake and Eligibility         | New assignment triage and eligibility checks      |
| WIOA Assignments     | Training Provider Handoffs     | Provider referrals, confirmations, and exceptions |
| WIOA Assignments     | Case Follow-up                 | Participant progress and required contact work    |
| Engineering Delivery | Assignment Workflow Automation | Product and backend automation                    |
| Engineering Delivery | Reporting and Compliance       | Reports, dashboards, exports                      |
| Engineering Delivery | Integrations                   | Partner/provider integrations                     |

Create one current cycle in each project:

| Project              | Cycle                      | Length  |
| -------------------- | -------------------------- | ------- |
| WIOA Assignments     | May WIOA Assignment Sprint | 2 weeks |
| Engineering Delivery | May Engineering Sprint     | 2 weeks |

Import or manually create the work items from [wioa-plane-demo-backlog.csv](./wioa-plane-demo-backlog.csv).

## Recommended Views

Create these saved views during setup or live during the demo:

| View                 | Project              | Filters                                     | Grouping |
| -------------------- | -------------------- | ------------------------------------------- | -------- |
| At Risk Assignments  | WIOA Assignments     | label is `risk` OR priority is urgent/high  | State    |
| Eligibility Queue    | WIOA Assignments     | label is `eligibility`                      | Assignee |
| Partner Handoffs     | WIOA Assignments     | label is `partner-handoff`                  | Module   |
| Engineering Blockers | Engineering Delivery | priority is urgent/high OR state is blocked | State    |
| Reporting Work       | Engineering Delivery | label is `reporting`                        | Module   |

## Demo Storyline

### 1. Open With The Operating Model

Show the workspace and explain the split:

- WIOA operations track participant-facing assignment work.
- Engineering tracks the systems work needed to reduce manual follow-up and improve compliance reporting.
- Shared labels connect operational problems to engineering work without mixing ownership.

### 2. Triage New WIOA Assignments

Open `WIOA Assignments`, then use the `Eligibility Queue` view.

Show:

- Each participant assignment is a work item.
- Labels identify eligibility, risk, partner handoff, and data quality.
- Modules separate intake, provider handoff, and follow-up work.
- Priority makes participant-impacting items visible.

Move one item from `Backlog` or `Todo` to `In Progress`.

Recommended work item:

`Verify eligibility packet for participant A-1042`

Talk track:

> The assignment is not just a task title. It carries acceptance criteria, due date, priority, and the handoff context needed by the counselor or coordinator.

### 3. Handle A Risk Item

Open the `At Risk Assignments` view.

Recommended work item:

`Resolve missing provider confirmation for participant A-1027`

Show:

- Priority is `urgent`.
- Label includes `risk` and `partner-handoff`.
- The work item belongs to `Training Provider Handoffs`.
- The owner can add comments and status updates.

Move the item to a blocked state if available, or leave it in progress and add a note:

```text
Waiting on provider confirmation. Escalated to partner contact; follow-up due by 2026-05-14.
```

### 4. Connect Operations To Engineering

Switch to `Engineering Delivery`.

Open the module `Assignment Workflow Automation`.

Recommended work item:

`Send automatic reminder when provider confirmation is missing`

Explain how this engineering item came from repeated operational blockers in the WIOA project.

Show:

- Labels `automation`, `partner-handoff`, and `risk`.
- Acceptance criteria that are testable.
- Cycle assignment to the current engineering sprint.

### 5. Show Reporting And Compliance Work

Open the `Reporting Work` view.

Recommended work item:

`Build weekly WIOA assignment status export`

Talk track:

> Program leads need a repeatable export that answers which assignments are pending, blocked, overdue, or missing eligibility data. Engineering owns the export mechanics; operations owns the underlying case updates.

### 6. Close With A Page

Create a Plane Page named `WIOA Assignment Operating Rhythm`.

Use this page outline:

```markdown
# WIOA Assignment Operating Rhythm

## Daily triage

- Review Eligibility Queue.
- Update At Risk Assignments.
- Confirm provider handoffs due in the next 48 hours.

## Twice-weekly engineering sync

- Review operational blockers that need automation or reporting support.
- Confirm delivery status for current Engineering Delivery cycle.

## Weekly program review

- Export assignment status.
- Review overdue and blocked work.
- Decide which process gaps become engineering work items.
```

Embed or link the five saved views above if the Plane instance supports it.

## Success Criteria

By the end of the demo, the audience should see:

- How WIOA assignments can be managed as structured, accountable work.
- How case-management risk becomes visible before deadlines are missed.
- How engineering work is tied directly to operational bottlenecks.
- How Plane views, modules, cycles, and pages create a repeatable operating rhythm.

## Local Plane Startup Reference

For a local demo from this repository:

```bash
cp .env.example .env
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
docker compose -f docker-compose-local.yml up -d
pnpm dev
```

Expected local services:

- Web app: `http://localhost:3000`
- Admin app: `http://localhost:3001`
- API: `http://localhost:8000`

Use the repository root commands from `AGENTS.md` for checks and builds.
