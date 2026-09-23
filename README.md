# Grill & Go — Digital Ordering & Fulfilment System

**Module:** Software Engineering — Coursework 2 (System Requirements & Technical Design Specification)
**Client:** Uncle Bob, Owner of "Grill & Go" (Orchard Road, Singapore)
**Submission Deadline:** Tuesday, 13 October 2026, 23:59 SGT

## 1. Project Overview

Grill & Go is a small-business Western food stall processing roughly 30,000
customer orders a month (~1,000/day), with sharp peaks during lunch
(12PM–2PM) and dinner (6PM–9PM) service. Long physical queues during these
windows are causing customer drop-off and kitchen bottlenecks.

This repository contains the consulting deliverables produced by our team:
a QR-code-based mobile ordering system with mandatory pre-kitchen payment
(PayNow / Credit Card), a Kitchen Display System (KDS) for order fulfilment,
a real-time stock-toggle feature for the Store Manager, and read-only BI
integration (Power BI / Tableau) against the transactional database.

## 2. Team & Role Allocation

| Git Handle | Full Name | Primary Role | Key Contributions |
| :--- | :--- | :--- | :--- |
| `@studentA-analyst` | [Student A Name] | Lead Systems Analyst | User Requirements Specification, User Stories, Use Case Diagram, Client Sign-Off, RTM |
| `@studentB-developer` | [Student B Name] | Software Architect / Lead Developer | C4 Architecture (C1/C2), Sequence Diagram, API Specifications |
| `@studentA-qa` | [Student A Name] | Integration & BI Specialist | Database Schema (ERD), NFRs, Power BI integration notes, QA review of both documents |

> Each member commits under their own distinct Git account. Commit history
> is used for individual moderation per the module's Git Commit Audit policy.

## 3. Repository Structure

```
grill-and-go-group-XX/
├── README.md                                  <- This file: team overview & role allocation
├── 01_User_Requirements_Specification.md      <- Document 1 (URS + Client Sign-off)
├── 02_Technical_Design_Specification.md       <- Document 2 (TDS + Developer Sign-off)
└── diagrams/                                  <- Diagram source files (PlantUML/Mermaid)
    ├── use_case_diagram.puml
    ├── c1_system_context.mmd
    ├── c2_container_diagram.mmd
    ├── sequence_order_payment.mmd
    └── erd_database_schema.mmd
```

## 4. Technology Stack Summary

| Layer | Technology Choice | Rationale |
| :--- | :--- | :--- |
| Customer Front-End | Mobile-responsive Single Page App (React + Vite), served via QR-code deep link — no app install required | Matches "scan QR → order in browser" constraint |
| KDS Front-End | Lightweight web app on Android tablet, polling/WebSocket-driven | Kitchen staff need near-real-time status updates |
| API Backend | REST API (Node.js/Express or Java Spring Boot) | Simple, well-understood, easy to scale horizontally behind a load balancer for 100 concurrent sessions |
| Database | PostgreSQL (managed relational DB) | ACID guarantees for payment-linked order data; native support for Power BI/Tableau ODBC connections |
| Payments | PayNow QR (SGQR) + Credit Card via a PCI-DSS-compliant gateway (e.g. Stripe) | Mandated by client; offloads card-data handling/PCI scope to the gateway |
| Analytics | Power BI / Tableau, read-only connection to a reporting replica of the DB | Client preference for off-the-shelf BI over custom dashboards |

## 5. How to Read This Repository

1. Start with `01_User_Requirements_Specification.md` for the business
   context, user stories, and the Use Case diagram.
2. Read `02_Technical_Design_Specification.md` for the C4 architecture,
   sequence diagram, ERD, API contracts, and the Requirements Traceability
   Matrix (RTM).
3. Diagram source files live in `diagrams/` — Mermaid (`.mmd`) files render
   natively on GitHub; PlantUML (`.puml`) files can be rendered via the
   [PlantUML online server](https://www.plantuml.com/plantuml) or a local
   PlantUML extension.

## 6. Version Control Conventions

- Commit messages follow `[DOC][SECTION] short description`, e.g.
  `[URS][UserStories] add kitchen staff status-update story`.
- Each team member works on a feature branch (`feature/<name>-<topic>`) and
  merges via Pull Request reviewed by at least one other team member.
- The `diagrams/` folder is updated in the same commit as the Markdown
  section that embeds/references the diagram, to keep docs and diagrams in
  sync.
