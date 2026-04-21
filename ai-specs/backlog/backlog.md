# Product Backlog: LTI — Next-Generation Applicant Tracking System

## Metadata

- **Source PRD**: `ai-specs/specs/PRD.md`
- **Generated**: 2026-04-21
- **Prioritization Method**: RICE Scoring (Reach × Impact × Confidence ÷ Effort)
- **Estimation Method**: Fibonacci Story Points + Planning Poker Consensus + T-Shirt Sizing
- **Total Stories**: 12
- **Total Story Points**: 107

---

## MVP Scope

The MVP (Release 1.0) includes all 8 **Must Have** stories (US-001 through US-006, US-008, US-010), totalling **73 story points** across approximately **8 two-week sprints** for a 4-person team.

The MVP delivers the full circular recruiting lifecycle: AI-assisted job creation → multi-channel publishing → AI-ranked candidate pipeline → real-time recruiter/manager collaboration → automated interview scheduling → structured scorecards → automated candidate notifications — all protected by role-based access control.

The 4 **Should Have** stories (US-007, US-009, US-011, US-012) are scoped to Release 1.5 (34 additional story points, ~4 sprints).

---

## Epics Overview

### Epic E-01: Foundation & Access Control
- **Description**: Multi-tenant authentication, RBAC permission model, audit logging, and SSO support. This is a technical prerequisite that all other epics depend on.
- **Business Objective**: B3 (customer trust), B5 (compliance/GDPR)
- **Stories**: US-010
- **Total Points**: 8
- **Priority**: Must Have

### Epic E-02: Job Management & AI-Assisted Creation
- **Description**: End-to-end job lifecycle from AI-drafted description through multi-channel publication to external job boards.
- **Business Objective**: B1 (reduce time-to-hire), B4 (reduce admin time)
- **Stories**: US-001, US-002
- **Total Points**: 21
- **Priority**: Must Have

### Epic E-03: Candidate Pipeline & AI Ranking
- **Description**: Application ingestion, AI CV parsing and ranking, screening forms, and pipeline stage management.
- **Business Objective**: B1 (reduce time-to-hire), B4 (reduce admin time)
- **Stories**: US-004, US-009
- **Total Points**: 21
- **Priority**: US-004 Must Have / US-009 Should Have

### Epic E-04: Real-Time Collaboration
- **Description**: Shared candidate profile workspace with threaded comments, @mentions, and real-time presence — replacing email-based recruiter/manager coordination.
- **Business Objective**: B2 (NPS), B4 (reduce admin time)
- **Stories**: US-003
- **Total Points**: 8
- **Priority**: Must Have

### Epic E-05: Interview Scheduling & Scorecards
- **Description**: Automated panel availability detection, candidate self-scheduling, structured scorecard collection, and debrief aggregation.
- **Business Objective**: B1 (reduce time-to-hire), B2 (NPS)
- **Stories**: US-005, US-006
- **Total Points**: 18
- **Priority**: Must Have

### Epic E-06: Candidate Communication & Notifications
- **Description**: Automated email/SMS notifications triggered by pipeline stage changes, with per-company customizable templates.
- **Business Objective**: B5 (candidate satisfaction)
- **Stories**: US-008
- **Total Points**: 5
- **Priority**: Must Have

### Epic E-07: Assessment Integration
- **Description**: Third-party technical/cognitive assessment dispatch and result ingestion via HackerRank and Codility integrations.
- **Business Objective**: B1 (reduce time-to-hire), B4 (reduce admin time)
- **Stories**: US-011
- **Total Points**: 8
- **Priority**: Should Have

### Epic E-08: HR Analytics & Reporting
- **Description**: Executive analytics dashboard with hiring funnel, time-to-hire, source attribution, and anonymized diversity metrics.
- **Business Objective**: B3 (customer milestone), B5 (HR director ROI)
- **Stories**: US-007
- **Total Points**: 13
- **Priority**: Should Have

### Epic E-09: Mobile Experience
- **Description**: Mobile-responsive hiring manager review flow enabling scorecard submission, candidate review, and comment threading on mobile devices.
- **Business Objective**: B2 (NPS), B4 (collaboration adoption)
- **Stories**: US-012
- **Total Points**: 5
- **Priority**: Should Have

---

## Prioritized Backlog

Ranked by RICE score (descending). Dependencies must be resolved before work begins.

| Rank | ID     | Title                                        | Epic  | Points | T-Shirt | MoSCoW | RICE  | Dependencies          |
|------|--------|----------------------------------------------|-------|--------|---------|--------|-------|-----------------------|
| 1    | US-010 | Role-Based Access Control (RBAC)             | E-01  | 8      | L       | Must   | 7.8   | —                     |
| 2    | US-001 | AI Job Description Generator                 | E-02  | 8      | L       | Must   | 9.6   | US-010                |
| 3    | US-004 | AI Candidate Ranking & Shortlisting          | E-03  | 13     | XL      | Must   | 9.1   | US-010                |
| 4    | US-008 | Automated Candidate Notifications            | E-06  | 5      | M       | Must   | 9.0   | US-010                |
| 5    | US-005 | Automated Interview Scheduling               | E-05  | 13     | XL      | Must   | 8.9   | US-004, US-010        |
| 6    | US-003 | Real-Time Collaboration Workspace            | E-04  | 8      | L       | Must   | 8.7   | US-004, US-010        |
| 7    | US-002 | Multi-Channel Job Publishing                 | E-02  | 13     | XL      | Must   | 8.4   | US-001                |
| 8    | US-006 | Structured Interview Scorecards              | E-05  | 5      | M       | Must   | 8.2   | US-005                |
| 9    | US-007 | HR Analytics Dashboard                       | E-08  | 13     | XL      | Should | 7.2   | US-004, US-005, US-008|
| 10   | US-012 | Mobile-Friendly Hiring Manager View          | E-09  | 5      | M       | Should | 7.0   | US-003, US-006        |
| 11   | US-009 | Automated Screening Question Forms           | E-03  | 8      | L       | Should | 6.8   | US-004, US-008        |
| 12   | US-011 | Online Assessment Integration                | E-07  | 8      | L       | Should | 6.4   | US-009                |

---

## Release Plan

### Phase 1 — MVP (Release 1.0)

**Goal**: Deliver the full circular recruiting lifecycle with AI and real-time collaboration.

| Sprint | Stories         | Points | Focus                                      |
|--------|-----------------|--------|--------------------------------------------|
| S-01   | US-010          | 8      | Auth, RBAC, multi-tenancy foundation       |
| S-02   | US-001          | 8      | AI JD generator + bias detection           |
| S-03   | US-004 (Part 1) | 7      | CV upload, S3 storage, parsing queue       |
| S-04   | US-004 (Part 2) | 6      | AI ranking engine, shortlist view          |
| S-05   | US-008, US-003  | 13     | Notifications + collaboration workspace    |
| S-06   | US-002          | 13     | Multi-channel job publishing               |
| S-07   | US-005          | 13     | Automated interview scheduling             |
| S-08   | US-006          | 5      | Structured scorecards + debrief view       |

**MVP Total**: 73 story points | 8 sprints | ~4 months (4-person team, 2-week sprints)

---

### Phase 2 — Release 1.5

**Goal**: Add analytics visibility, mobile access, screening forms, and assessment integrations.

| Sprint | Stories         | Points | Focus                                          |
|--------|-----------------|--------|------------------------------------------------|
| S-09   | US-007 (Part 1) | 7      | Funnel + time-to-hire analytics                |
| S-10   | US-007 (Part 2) | 6      | Source attribution + diversity metrics + export|
| S-11   | US-009, US-012  | 13     | Screening forms + mobile-responsive manager UX |
| S-12   | US-011          | 8      | HackerRank/Codility assessment integration     |

**Release 1.5 Total**: 34 story points | 4 sprints | ~2 months

---

### Phase 3 — Release 2.0 (Post-backlog)

- Offer letter generation + e-signature integration
- Employee referral portal
- Internal mobility / talent pool module
- Advanced bias detection with EEO reporting
- Slack / Teams notification integration
- Chrome extension for LinkedIn profile import

---

## Dependency Map

```
US-010 (RBAC)
  ├── US-001 (AI JD Generator)
  │     └── US-002 (Multi-Channel Publishing)
  ├── US-004 (AI Candidate Ranking)
  │     ├── US-005 (Interview Scheduling)
  │     │     └── US-006 (Scorecards)
  │     │           └── US-012 (Mobile Manager View)
  │     ├── US-009 (Screening Forms)
  │     │     └── US-011 (Assessment Integration)
  │     └── US-007 (Analytics Dashboard) ← also depends on US-005, US-008
  └── US-008 (Notifications)
        └── US-009 (Screening Forms)
  US-003 (Collaboration Workspace) ← depends on US-004, US-010
```

---

## Risks & Assumptions

### Risks

| ID | Risk | Affected Stories | Mitigation |
|----|------|-----------------|------------|
| R-01 | AI ranking model cold-start: insufficient training data for new customers | US-004 | Use global pre-trained model as baseline; fine-tune per org after 50+ applications |
| R-02 | Calendar OAuth token management complexity (Google + Outlook) | US-005 | Ship Google Calendar only in MVP; Outlook in Release 1.5; manual fallback always available |
| R-03 | Job board API rate limits and schema changes | US-002 | Abstract behind adapter layer; implement retry/backoff queue; monitor via webhook status |
| R-04 | GDPR consent flow must be in place before any AI processing | US-004, US-009, US-011 | US-010 (RBAC) sprint must include GDPR consent infrastructure as mandatory sub-task |
| R-05 | Real-time WebSocket complexity under high concurrent load | US-003 | Use Redis pub/sub as message bus across API replicas; load test at 1,000 concurrent users pre-launch |
| R-06 | Assessment provider API instability or rate limits | US-011 | Webhook-first architecture; result polling fallback; graceful degradation (show "pending" state) |

### Backlog Assumptions

- A-01: US-010 (RBAC) includes GDPR consent tracking infrastructure — this is a hard dependency for all AI-touching stories.
- A-02: CV parsing uses the Anthropic Claude API (structured extraction prompt) rather than a separate ML model — reduces infrastructure complexity at the cost of slightly higher per-parse cost.
- A-03: Multi-channel publishing (US-002) uses a queue-based async pattern; the UI shows per-channel status (pending/live/failed) rather than waiting for all publishes to complete synchronously.
- A-04: The real-time collaboration (US-003) uses Redis pub/sub for event broadcast; SSE (Server-Sent Events) is the fallback if WebSocket connections are blocked by enterprise firewalls.
- A-05: Analytics (US-007) reads from a PostgreSQL read replica from day one — the primary DB must be provisioned with replication before Sprint S-09 begins.
