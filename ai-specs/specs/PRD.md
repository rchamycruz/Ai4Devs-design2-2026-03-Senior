# Product Requirements Document: LTI — Next-Generation Applicant Tracking System

| Field       | Value                              |
|-------------|-----------------------------------|
| Version     | 1.0                               |
| Date        | 2026-04-20                        |
| Author      | AI-assisted (product-manager-ba)  |
| Status      | Draft                             |

---

## 1. Executive Summary

LTI is a next-generation Applicant Tracking System (ATS) built for modern HR teams that are drowning in manual processes, disconnected tools, and slow hiring cycles. Traditional ATS platforms are rigid, data-poor, and offer zero real-time collaboration — LTI flips this model by embedding AI throughout the entire recruiting lifecycle, from job creation to offer acceptance.

The platform covers every phase of the circular recruiting process: job creation, multi-channel publishing, application collection, AI-assisted review, automated online assessments, interview scheduling, and final hiring decisions. Each phase feeds data back into the system, continuously improving hiring quality and team efficiency.

LTI's competitive edge rests on three pillars: (1) AI co-pilot capabilities that surface ranked candidates, draft job descriptions, and flag biased language; (2) a real-time collaboration workspace where recruiters and hiring managers work side-by-side within the platform instead of over email; and (3) a deeply automated pipeline that eliminates repetitive tasks — screening emails, interview reminders, assessment dispatch — so HR teams focus on human judgment, not logistics.

### Problem Statement

Recruiting teams spend an estimated 60–70% of their time on administrative tasks: parsing CVs, scheduling interviews, chasing feedback from managers, and manually updating spreadsheets. Existing ATS tools were designed for pre-AI, pre-collaboration-software eras and have not evolved meaningfully. The result is slow time-to-hire, poor candidate experience, and inconsistent decision quality.

### Target Audience

Primary: HR/Talent Acquisition teams in mid-market companies (50–2,000 employees) looking to modernize their hiring stack. Secondary: Hiring managers who need lightweight collaboration access without full ATS training.

---

## 2. Product Vision & Objectives

### Vision Statement

> "Empower every hiring team to find, evaluate, and hire exceptional talent faster — with AI as a co-pilot and collaboration as the engine."

### Business Objectives

| # | Objective | Target | Timeline |
|---|-----------|--------|----------|
| B1 | Reduce average time-to-hire for customers | ≥ 30% reduction vs. baseline | 12 months post-launch |
| B2 | Achieve Net Promoter Score (NPS) from HR teams | ≥ 50 | 6 months post-launch |
| B3 | Reach paying customer milestone | 100 companies | 9 months post-launch |
| B4 | Reduce recruiter administrative time | ≥ 40% reduction | 12 months post-launch |
| B5 | Candidate satisfaction score (post-process survey) | ≥ 4.2 / 5.0 | 12 months post-launch |

### Success Metrics (KPIs)

- **Time-to-hire**: Days from job creation to accepted offer
- **Pipeline conversion rate**: % of applicants advancing through each stage
- **Recruiter efficiency**: Number of open reqs managed per recruiter
- **AI recommendation accuracy**: % of AI-ranked top-5 candidates that reach final interview
- **Collaboration adoption**: % of hiring decisions with ≥ 1 manager comment in the platform
- **System uptime**: 99.9% availability SLA

### Strategic Alignment

LTI targets the USD 3.2B ATS market (2025), with the AI-augmented HR tech segment growing at 18% CAGR. The product is positioned to displace legacy tools (Workday, Greenhouse, Lever) in the mid-market segment by offering AI features previously only accessible to enterprise buyers.

---

## 3. Target Users & Personas

### Persona 1 — Sarah, the Recruiter

| Attribute | Detail |
|-----------|--------|
| Role | In-house Recruiter / Talent Acquisition Specialist |
| Company size | 200–800 employees |
| Age | 28–38 |
| Tech fluency | High |
| Goals | Fill open roles fast, maintain quality bar, keep candidates warm |
| Pain points | Too many tools (ATS + email + spreadsheet + calendar), slow manager feedback, CV parsing errors, chasing status updates |
| Current alternatives | Greenhouse, Workday, or Excel + email |

**Key needs:** AI-ranked candidate lists, one-click calendar scheduling, status dashboards, templated comms.

---

### Persona 2 — Marco, the Hiring Manager

| Attribute | Detail |
|-----------|--------|
| Role | Engineering Manager / Department Head |
| Company size | 100–2,000 employees |
| Age | 32–45 |
| Tech fluency | Medium |
| Goals | Hire strong contributors without being pulled into admin work |
| Pain points | Email threads with no context, missing scorecards, no visibility into pipeline until final stage |
| Current alternatives | Email + shared Google Docs + calendar invites |

**Key needs:** Simple candidate review interface, scorecard submission, interview feedback history, mobile-friendly.

---

### Persona 3 — Diana, the HR Director

| Attribute | Detail |
|-----------|--------|
| Role | Head of HR / People Operations Director |
| Company size | 500–2,000 employees |
| Age | 38–52 |
| Tech fluency | Medium |
| Goals | Reduce cost-per-hire, ensure compliance (GDPR, equal opportunity), demonstrate ROI of HR function |
| Pain points | No aggregate analytics, inconsistent process across teams, compliance risks with manual data |
| Current alternatives | HRIS reporting modules, custom dashboards built by BI team |

**Key needs:** Hiring analytics dashboard, diversity/equity metrics, audit trail, role-based access control.

---

### Persona 4 — Alex, the Candidate

| Attribute | Detail |
|-----------|--------|
| Role | Job Applicant |
| Age | 22–45 |
| Tech fluency | Medium–High |
| Goals | Understand application status, complete assessments easily, receive timely communication |
| Pain points | Black-hole applications, inconsistent communication, clunky assessment tools |
| Current alternatives | Company career portals, LinkedIn Easy Apply |

**Key needs:** Application status tracking, mobile-responsive experience, clear next-step notifications.

---

## 4. Use Cases & User Stories

### Use Case 1 — Job Creation & Publication

**Actors:** Recruiter (primary), Hiring Manager (reviewer), AI System  
**Preconditions:** Recruiter is authenticated; job requisition is approved internally  
**Main Flow:**
1. Recruiter initiates "New Job" from the dashboard
2. AI co-pilot suggests job title normalization and draft description based on role type
3. Recruiter edits description; AI flags gender-coded or exclusive language in real time
4. Recruiter sets requirements: location, experience level, compensation range (optional), skills tags
5. Hiring Manager is notified to review and approve the job post (in-platform comment thread)
6. Once approved, Recruiter selects publication channels: company career page, LinkedIn, Indeed, internal board
7. System auto-publishes and tracks source for each application received

**Postconditions:** Job is live on selected channels; pipeline is open; source tracking is active  
**Alternative Flow:** Manager requests edits → Recruiter revises → re-approval cycle  
**Exception Flow:** Publishing API for job board fails → system queues retry and notifies Recruiter

---

### Use Case 2 — Candidate Screening & Collaboration

**Actors:** Recruiter, Hiring Manager, AI System  
**Preconditions:** Job is published; applications have been received  
**Main Flow:**
1. AI parses incoming CVs and extracts structured data (skills, experience, education)
2. AI scores and ranks candidates against job requirements; surfacing a "top matches" shortlist
3. Recruiter reviews AI shortlist; can accept, reject, or override ranking with justification
4. Recruiter shares shortlist with Hiring Manager via in-platform collaboration thread
5. Hiring Manager views candidate profiles, leaves comments, and submits initial recommendation
6. Recruiter moves approved candidates to "Phone Screen" stage; system auto-sends invite email from template
7. After phone screen, Recruiter logs outcome and advances or rejects the candidate

**Postconditions:** Candidates are in the appropriate pipeline stage; all decisions are logged  
**Alternative Flow:** Recruiter disagrees with AI ranking → marks candidates manually; AI learns from correction  
**Exception Flow:** Candidate is already in system (duplicate) → system flags and merges profiles

---

### Use Case 3 — Interview Scheduling & Decision

**Actors:** Recruiter, Hiring Manager, Interviewer Panel, Candidate  
**Preconditions:** Candidate has passed screening; interview panel is defined  
**Main Flow:**
1. Recruiter triggers "Schedule Interview" for a candidate
2. System reads calendar availability of all panel members (Google Calendar / Outlook integration) and proposes 3 time slots
3. Recruiter sends self-scheduling link to candidate
4. Candidate selects preferred slot; calendar invites are auto-created for all parties
5. System sends reminder notifications 24h and 1h before interview
6. Each interviewer submits a structured scorecard within the platform post-interview
7. System aggregates scores and presents to Recruiter and Hiring Manager in a debrief view
8. Hiring team reaches consensus (in-platform); Hiring Manager approves hire decision
9. Recruiter triggers offer generation; system logs hire event and closes the pipeline

**Postconditions:** Candidate is hired; pipeline closes; analytics updated; onboarding handoff triggered  
**Alternative Flow:** Candidate reschedules → system re-proposes slots from updated availability  
**Exception Flow:** Calendar integration fails → manual slot entry with system reminders still active

---

### Selected User Stories

| ID | User Story | Priority | Acceptance Criteria |
|----|-----------|----------|---------------------|
| US-001 | As a Recruiter, I want AI to generate a draft job description from a role title, so that I can reduce drafting time by 70%. | Must | AI generates a draft in < 3s; draft is editable; bias detection flags appear inline |
| US-002 | As a Recruiter, I want to publish a job to multiple boards in one click, so that I reach more candidates without duplicating effort. | Must | Publish to ≥ 3 external boards simultaneously; source is tagged per application |
| US-003 | As a Hiring Manager, I want to review candidate profiles and leave comments, so that I can collaborate with the recruiter asynchronously. | Must | Manager can access shared view; comments are timestamped and attributed; recruiter receives notification |
| US-004 | As a Recruiter, I want to see AI-ranked candidate shortlists, so that I can prioritize review of the best-fit applicants. | Must | AI rank visible on each candidate card; ranking rationale is explainable; recruiter can override |
| US-005 | As a Recruiter, I want the system to propose available interview slots from panel calendars, so that I can eliminate back-and-forth scheduling. | Must | Slots pulled from connected calendars; candidate self-scheduling link generated; invites auto-sent |
| US-006 | As an Interviewer, I want to submit a structured scorecard after each interview, so that feedback is consistent and actionable. | Must | Scorecard template per role type; mandatory fields enforced; submitted within 24h window |
| US-007 | As an HR Director, I want a hiring analytics dashboard, so that I can track time-to-hire, source effectiveness, and diversity metrics. | Should | Dashboard shows: time-to-hire by role/team, source conversion, gender/seniority distribution; exportable |
| US-008 | As a Candidate, I want to receive automated status updates at each stage change, so that I am never left wondering about my application. | Must | Email/SMS notification sent within 5 min of stage change; template is customizable by company |
| US-009 | As a Recruiter, I want automated screening question forms dispatched to applicants, so that I can filter candidates without manual outreach. | Should | Form linked to job; responses stored; AI summarizes answers per candidate |
| US-010 | As an HR Director, I want role-based access control, so that sensitive candidate data is only visible to authorized users. | Must | Permissions enforced at API and UI level; audit log captures all data access events |
| US-011 | As a Recruiter, I want to trigger online assessments for shortlisted candidates, so that I can evaluate technical or cognitive skills before interviews. | Should | Assessment provider integration (e.g., HackerRank, Codility); results displayed in candidate profile |
| US-012 | As a Hiring Manager, I want a mobile-friendly candidate review interface, so that I can review profiles and leave feedback from my phone. | Should | PWA or responsive design; full scorecard submission works on mobile; loads in < 2s on 4G |

---

## 5. Key Features & Functional Requirements

### F-001 — AI Job Description Generator

| Field | Detail |
|-------|--------|
| Description | AI generates a structured job description draft from role title + level inputs |
| Linked US | US-001 |
| Acceptance Criteria | Draft generated in < 3s; includes summary, responsibilities, requirements, nice-to-haves; bias flags inline |
| Dependencies | LLM API (Claude/GPT), Job taxonomy dataset |
| Priority | Must Have |
| Complexity | Medium |

---

### F-002 — Multi-Channel Job Publishing

| Field | Detail |
|-------|--------|
| Description | One-click publication to company career page and external job boards (LinkedIn, Indeed, Glassdoor) |
| Linked US | US-002 |
| Acceptance Criteria | Simultaneous publish to ≥ 3 channels; source UTM tagging per channel; status per channel shown |
| Dependencies | Job board APIs, company career page CMS integration |
| Priority | Must Have |
| Complexity | High |

---

### F-003 — AI Candidate Ranking & Shortlisting

| Field | Detail |
|-------|--------|
| Description | ML model scores each applicant against job requirements and surfaces a ranked shortlist |
| Linked US | US-004 |
| Acceptance Criteria | Rank + explainability label per candidate; override capability; model retrains from recruiter corrections |
| Dependencies | CV parsing engine, job requirement schema, ML inference service |
| Priority | Must Have |
| Complexity | High |

---

### F-004 — Real-Time Collaboration Workspace

| Field | Detail |
|-------|--------|
| Description | Shared candidate profile view where recruiters and managers can comment, tag, and react in real time |
| Linked US | US-003 |
| Acceptance Criteria | Comments attributed + timestamped; @mention notifications; activity feed per candidate |
| Dependencies | WebSocket service, notification service |
| Priority | Must Have |
| Complexity | Medium |

---

### F-005 — Automated Interview Scheduling

| Field | Detail |
|-------|--------|
| Description | System reads panel calendars, proposes slots, sends self-scheduling link to candidate, creates calendar events |
| Linked US | US-005 |
| Acceptance Criteria | ≥ 3 slots proposed; calendar events auto-created; reminders sent at 24h and 1h; reschedule flow supported |
| Dependencies | Google Calendar API, Microsoft Graph API, email/SMS notification service |
| Priority | Must Have |
| Complexity | High |

---

### F-006 — Structured Interview Scorecards

| Field | Detail |
|-------|--------|
| Description | Configurable scorecard templates per role; submitted by each interviewer; aggregated in debrief view |
| Linked US | US-006 |
| Acceptance Criteria | Template builder with rating scales + free text; submission enforced pre-decision; debrief view with average scores |
| Dependencies | Form builder, notification service |
| Priority | Must Have |
| Complexity | Medium |

---

### F-007 — Candidate Communication Automation

| Field | Detail |
|-------|--------|
| Description | Automated email/SMS notifications triggered by pipeline stage changes; customizable templates per company |
| Linked US | US-008 |
| Acceptance Criteria | Notification sent within 5 min of stage change; template editor with merge tags; opt-out compliance |
| Dependencies | Email provider (SendGrid/SES), SMS provider (Twilio), template engine |
| Priority | Must Have |
| Complexity | Medium |

---

### F-008 — HR Analytics Dashboard

| Field | Detail |
|-------|--------|
| Description | Executive dashboard showing hiring funnel, time-to-hire, source effectiveness, and diversity metrics |
| Linked US | US-007 |
| Acceptance Criteria | Real-time data; filterable by team/role/time range; CSV export; diversity data anonymized by default |
| Dependencies | Data warehouse, BI visualization layer |
| Priority | Should Have |
| Complexity | High |

---

### F-009 — Online Assessment Integration

| Field | Detail |
|-------|--------|
| Description | Dispatch technical/cognitive assessments to candidates via third-party integrations; results in candidate profile |
| Linked US | US-011 |
| Acceptance Criteria | Integration with ≥ 2 assessment providers; result ingestion < 1h; AI summary of results |
| Dependencies | Assessment provider webhooks (HackerRank, Codility) |
| Priority | Should Have |
| Complexity | Medium |

---

### F-010 — Role-Based Access Control (RBAC)

| Field | Detail |
|-------|--------|
| Description | Configurable permission model: Admin, HR Director, Recruiter, Hiring Manager, Interviewer, View-Only |
| Linked US | US-010 |
| Acceptance Criteria | Permissions enforced at API and UI; audit log for all data access; GDPR-compliant data minimization |
| Dependencies | Auth service (OAuth 2.0 / SSO), audit logging service |
| Priority | Must Have |
| Complexity | Medium |

---

## 6. Data Model

### Core Entities

#### Organization
- `id` UUID PK
- `name` VARCHAR(255)
- `domain` VARCHAR(255)
- `plan` ENUM(starter, growth, enterprise)
- `created_at` TIMESTAMP
- `settings` JSONB

#### User
- `id` UUID PK
- `organization_id` UUID FK → Organization
- `email` VARCHAR(255) UNIQUE
- `full_name` VARCHAR(255)
- `role` ENUM(admin, hr_director, recruiter, hiring_manager, interviewer, view_only)
- `avatar_url` VARCHAR(500)
- `is_active` BOOLEAN
- `last_login_at` TIMESTAMP

#### Job
- `id` UUID PK
- `organization_id` UUID FK → Organization
- `title` VARCHAR(255)
- `description_html` TEXT
- `location` VARCHAR(255)
- `employment_type` ENUM(full_time, part_time, contract, internship)
- `experience_level` ENUM(junior, mid, senior, lead, executive)
- `status` ENUM(draft, open, paused, closed)
- `created_by` UUID FK → User
- `hiring_manager_id` UUID FK → User
- `published_at` TIMESTAMP
- `closed_at` TIMESTAMP
- `created_at` TIMESTAMP
- `salary_min` INTEGER
- `salary_max` INTEGER
- `currency` CHAR(3)
- `tags` TEXT[]

#### JobPublication
- `id` UUID PK
- `job_id` UUID FK → Job
- `channel` ENUM(career_page, linkedin, indeed, glassdoor, internal)
- `external_id` VARCHAR(255) — board-assigned job ID
- `published_at` TIMESTAMP
- `status` ENUM(pending, live, expired, failed)

#### Candidate
- `id` UUID PK
- `email` VARCHAR(255)
- `full_name` VARCHAR(255)
- `phone` VARCHAR(50)
- `linkedin_url` VARCHAR(500)
- `location` VARCHAR(255)
- `created_at` TIMESTAMP
- `gdpr_consent_at` TIMESTAMP
- `gdpr_consent_ip` VARCHAR(45)

#### Application
- `id` UUID PK
- `job_id` UUID FK → Job
- `candidate_id` UUID FK → Candidate
- `source` ENUM(career_page, linkedin, indeed, glassdoor, referral, direct)
- `stage` ENUM(applied, screening, phone_screen, assessment, interview, offer, hired, rejected, withdrawn)
- `ai_score` FLOAT — 0–100 ranking from AI engine
- `ai_score_rationale` JSONB
- `applied_at` TIMESTAMP
- `updated_at` TIMESTAMP
- `rejection_reason` VARCHAR(255)
- `resume_url` VARCHAR(500)
- `cover_letter_url` VARCHAR(500)

#### ApplicationNote
- `id` UUID PK
- `application_id` UUID FK → Application
- `author_id` UUID FK → User
- `content` TEXT
- `created_at` TIMESTAMP
- `mention_ids` UUID[]

#### Interview
- `id` UUID PK
- `application_id` UUID FK → Application
- `scheduled_at` TIMESTAMP
- `duration_minutes` INTEGER
- `interview_type` ENUM(phone, video, onsite, panel)
- `status` ENUM(scheduled, completed, cancelled, rescheduled)
- `meeting_url` VARCHAR(500)
- `calendar_event_ids` JSONB

#### InterviewerAssignment
- `id` UUID PK
- `interview_id` UUID FK → Interview
- `user_id` UUID FK → User
- `role` ENUM(lead, panelist, observer)

#### Scorecard
- `id` UUID PK
- `interview_id` UUID FK → Interview
- `interviewer_id` UUID FK → User
- `overall_rating` ENUM(strong_yes, yes, neutral, no, strong_no)
- `scores` JSONB — array of {criteria, rating, comment}
- `submitted_at` TIMESTAMP
- `hire_recommendation` BOOLEAN

#### Assessment
- `id` UUID PK
- `application_id` UUID FK → Application
- `provider` ENUM(hackerrank, codility, custom)
- `external_id` VARCHAR(255)
- `sent_at` TIMESTAMP
- `completed_at` TIMESTAMP
- `score` FLOAT
- `report_url` VARCHAR(500)
- `ai_summary` TEXT

#### Notification
- `id` UUID PK
- `recipient_type` ENUM(candidate, user)
- `recipient_id` UUID
- `channel` ENUM(email, sms, in_app)
- `template_id` VARCHAR(100)
- `payload` JSONB
- `sent_at` TIMESTAMP
- `status` ENUM(queued, sent, delivered, failed)

### Key Relationships

- **Organization** 1:N **User**, **Job**
- **Job** 1:N **JobPublication**, **Application**
- **Candidate** 1:N **Application**
- **Application** 1:N **ApplicationNote**, **Interview**, **Assessment**
- **Interview** 1:N **InterviewerAssignment**, **Scorecard**

### Data Privacy & Retention

- Candidate PII is encrypted at rest (AES-256)
- GDPR right-to-erasure: anonymization pipeline triggered on request; `candidate_id` replaced with hashed token in historical records
- Application data retained 2 years after job closure (configurable per organization)
- Audit logs retained 7 years for compliance

---

## 7. System Architecture (High-Level)

### Architecture Overview

LTI follows a **modular monolith** architecture for v1, designed to extract services independently as scale demands. The system is organized around five primary domains:

```
┌─────────────────────────────────────────────────────┐
│                    Client Layer                      │
│  Web App (React SPA)  |  Mobile PWA  |  Email/SMS   │
└──────────────┬──────────────────────────────────────┘
               │ HTTPS / WebSocket
┌──────────────▼──────────────────────────────────────┐
│               API Gateway (REST + WS)                │
│  Auth (JWT/SSO)  |  Rate Limiting  |  API Versioning │
└──────────────┬──────────────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────┐
│              Application Core (Node.js / TypeScript) │
│                                                      │
│  ┌─────────┐ ┌──────────┐ ┌──────────┐ ┌─────────┐ │
│  │  Jobs   │ │ Pipeline │ │Scheduling│ │Collab.  │ │
│  │ Module  │ │ Module   │ │ Module   │ │ Module  │ │
│  └─────────┘ └──────────┘ └──────────┘ └─────────┘ │
│  ┌─────────┐ ┌──────────┐ ┌──────────┐             │
│  │  Auth   │ │Analytics │ │Notif.    │             │
│  │ Module  │ │ Module   │ │ Module   │             │
│  └─────────┘ └──────────┘ └──────────┘             │
└──────────────┬──────────────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────┐
│                   AI Services Layer                  │
│  CV Parser  |  Candidate Ranker  |  JD Generator    │
│  (Python microservice — async via message queue)     │
└──────────────┬──────────────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────┐
│                   Data Layer                         │
│  PostgreSQL (primary)  |  Redis (cache/sessions)     │
│  S3-compatible (resumes/assets)  |  Event Log (JSONL)│
└──────────────┬──────────────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────┐
│               External Integrations                  │
│  Job Boards  |  Calendar APIs  |  Email/SMS          │
│  Assessment Providers  |  SSO (SAML/OIDC)           │
└─────────────────────────────────────────────────────┘
```

### Technology Stack Recommendations

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Frontend | React 19 + TypeScript + Tailwind CSS | Component ecosystem, type safety, rapid UI dev |
| Backend | Node.js + TypeScript (Fastify) | Shared language with frontend, strong ecosystem, performance |
| AI Services | Python (FastAPI) + Anthropic Claude API | Best-in-class LLM for text generation and analysis |
| Primary DB | PostgreSQL 17 | Relational integrity, JSONB for flexible fields, mature |
| Cache | Redis 7 | Session store, real-time pub/sub for collaboration |
| Queue | BullMQ (Redis-backed) | Job processing for CV parsing, notifications, AI tasks |
| File Storage | AWS S3 / Cloudflare R2 | Scalable object storage for resumes and assets |
| Auth | Auth0 / Clerk (OIDC + SAML SSO) | Enterprise SSO support out of the box |
| Email | SendGrid | Reliable delivery, template management |
| SMS | Twilio | Global SMS delivery |
| Hosting | AWS ECS (Fargate) + RDS + ElastiCache | Managed, scalable, standard enterprise cloud |
| CI/CD | GitHub Actions | Automated test → build → deploy pipeline |

### Integration Points

- **Google Calendar & Microsoft Graph API** — interview availability and event creation
- **LinkedIn Jobs API, Indeed Publisher API, Glassdoor Employer API** — multi-channel posting
- **HackerRank API, Codility API** — assessment dispatch and result ingestion
- **Anthropic Claude API** — JD generation, bias detection, CV analysis, candidate ranking rationale
- **SAML 2.0 / OIDC providers** — enterprise SSO (Okta, Azure AD, Google Workspace)
- **Webhook endpoints** — inbound events from job boards and assessment providers

### Scalability Considerations

- Stateless API tier enables horizontal scaling behind a load balancer
- AI workloads decoupled via async queue; worker instances scale independently
- Database read replicas for analytics queries to avoid OLTP contention
- CDN-delivered frontend assets and resume/document files
- Target: support 10,000 concurrent users with < 200ms p99 API response time

---

## 8. API Specification (High-Level)

All endpoints are prefixed with `/api/v1`. Authentication via Bearer JWT required unless noted.

### Jobs

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/jobs` | List jobs for organization (filterable) |
| POST | `/jobs` | Create a new job |
| GET | `/jobs/:id` | Get job details |
| PATCH | `/jobs/:id` | Update job |
| POST | `/jobs/:id/publish` | Publish to selected channels |
| POST | `/jobs/:id/close` | Close job |
| POST | `/jobs/ai/generate-description` | AI-generated JD draft |

### Applications

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/jobs/:jobId/applications` | List applications for a job |
| POST | `/jobs/:jobId/applications` | Submit new application (public, no auth) |
| GET | `/applications/:id` | Get full application profile |
| PATCH | `/applications/:id/stage` | Move application to new stage |
| POST | `/applications/:id/notes` | Add collaboration note |
| GET | `/applications/:id/notes` | List notes for application |

### Interviews

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/applications/:id/interviews` | Schedule interview |
| GET | `/interviews/:id` | Get interview details |
| PATCH | `/interviews/:id` | Update / reschedule |
| POST | `/interviews/:id/scorecards` | Submit scorecard |
| GET | `/interviews/:id/scorecards` | Get aggregated scorecards |

### Candidates (Candidate-facing, partial auth)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/candidates/status/:token` | Get application status (token-auth) |
| POST | `/candidates/schedule/:token` | Self-schedule interview slot |

### Analytics

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/analytics/funnel` | Hiring funnel conversion by job/team |
| GET | `/analytics/time-to-hire` | Time-to-hire breakdown |
| GET | `/analytics/sources` | Source effectiveness report |
| GET | `/analytics/diversity` | Anonymized diversity metrics |

---

## 9. Non-Functional Requirements

### Performance

- API response time: p50 < 100ms, p99 < 500ms for read endpoints; p99 < 1,000ms for write endpoints
- AI generation endpoints: p50 < 3s, p99 < 8s
- Dashboard page load: < 2s on broadband, < 4s on 4G
- CV parsing queue: 95% of documents processed within 60s of submission

### Security

- All data encrypted in transit (TLS 1.3) and at rest (AES-256)
- OWASP Top 10 mitigations applied and verified via automated scanning in CI
- Authentication: JWT with short-lived access tokens (15 min) + refresh tokens (7 days); SSO via SAML 2.0/OIDC
- RBAC enforced at both API middleware and database row level (where applicable)
- GDPR compliance: consent tracking, data minimization, right-to-erasure, DPA-ready
- SOC 2 Type II roadmap: audit logging, penetration testing, vendor management

### Scalability

- System must support 10,000 concurrent active users without degradation
- CV parsing and AI workloads handled asynchronously; queue depth < 500 items under normal load
- Database must support 50M+ application records with query performance maintained via indexing strategy

### Availability & Reliability

- Target uptime: 99.9% (< 8.7h downtime/year)
- Automated health checks with PagerDuty alerting
- Database: Multi-AZ deployment; daily automated backups with 30-day retention; point-in-time recovery
- Zero-downtime deployments via blue/green or rolling strategy

### Accessibility

- WCAG 2.1 Level AA compliance for all candidate-facing and recruiter-facing screens
- Keyboard navigation fully supported
- Screen reader compatibility tested with NVDA and VoiceOver

### Internationalization

- v1: English only
- v1.5 target: Spanish, French, Portuguese (Brazilian)
- Date/time displayed in user's timezone; stored in UTC
- Currency display localized; amounts stored in minor units (cents)

---

## 10. UX/UI Guidelines

### Design Principles

1. **Clarity over density** — Show only what's needed for the current task; progressive disclosure for detail
2. **AI as assistant, not authority** — AI suggestions are always overridable; rationale is always visible
3. **Collaboration first** — Every candidate-facing view is designed for sharing and comment, not solo review
4. **Speed for power users** — Keyboard shortcuts for common recruiter actions; bulk operations supported

### Key Screens

1. **Pipeline Board** — Kanban view of candidates by stage for a job; drag-and-drop stage advancement; AI score badge; quick comment icon
2. **Candidate Profile** — Full CV view + structured data panel + AI analysis panel + note thread + interview history + scorecard aggregation
3. **Job Creator** — Split-pane: form on left, AI-assisted preview on right; bias warnings inline
4. **Interview Scheduler** — Calendar grid showing panel availability overlaps; slot selector; candidate link generator
5. **Analytics Dashboard** — Top-level cards (open roles, time-to-hire avg, hires this quarter) + funnel chart + source breakdown + diversity breakdown
6. **Scorecard Form** — Clean, focused rating form; one criterion at a time on mobile; progress indicator

### Navigation Flow

```
Dashboard
├── Jobs
│   ├── Job List → Job Detail → Pipeline Board → Candidate Profile
│   └── New Job → Job Creator (AI-assisted)
├── Candidates (global search)
├── Interviews (calendar view)
├── Analytics
└── Settings (RBAC, templates, integrations)
```

### Responsive Design

- Full feature parity on desktop (primary use case)
- Hiring Manager review flow fully functional on mobile (scorecard, comments, shortlist review)
- Candidate-facing screens (status, self-scheduling) mobile-first

---

## 11. Product Backlog

### Prioritization Methodology: MoSCoW + RICE

RICE scores used for Must/Should tier differentiation:
- **Reach**: estimated users per quarter
- **Impact**: 1–5 scale
- **Confidence**: % confidence in estimates
- **Effort**: person-weeks

### MVP (Release 1.0) — Must Have

| ID | Story | RICE Score | Story Points |
|----|-------|-----------|--------------|
| US-001 | AI JD Generator | 9.6 | 8 |
| US-002 | Multi-Channel Publishing | 8.4 | 13 |
| US-004 | AI Candidate Ranking | 9.1 | 13 |
| US-003 | Collaboration Workspace | 8.7 | 8 |
| US-005 | Automated Interview Scheduling | 8.9 | 13 |
| US-006 | Structured Scorecards | 8.2 | 5 |
| US-008 | Automated Candidate Notifications | 9.0 | 5 |
| US-010 | RBAC | 7.8 | 8 |

**MVP Estimated Effort:** ~73 story points (~8 sprints, 4-person team)

### Release 1.5 — Should Have

| ID | Story | RICE Score | Story Points |
|----|-------|-----------|--------------|
| US-007 | HR Analytics Dashboard | 7.2 | 13 |
| US-009 | Screening Question Forms | 6.8 | 8 |
| US-011 | Online Assessment Integration | 6.4 | 8 |
| US-012 | Mobile-Friendly Manager View | 7.0 | 5 |

### Release 2.0 — Could Have (Post-MVP)

- Offer letter generation and e-signature integration
- Employee referral portal
- Internal mobility / talent pool module
- Advanced bias detection with EEO reporting
- Slack / Teams integration for notifications
- Chrome extension for LinkedIn profile import

### Won't Have (v1)

- Full HRIS integration (payroll, onboarding modules)
- Video interviewing native recording (rely on Zoom/Teams)
- AI-generated interview questions (privacy/legal complexity)

### Key Dependencies

- US-005 (scheduling) depends on calendar integration being complete before US-006 (scorecards) is testable end-to-end
- US-004 (AI ranking) depends on CV parsing service being stable
- US-007 (analytics) depends on pipeline event schema being finalized in US-004 / US-005

---

## 12. Risks & Assumptions

### Risks

| ID | Risk | Probability | Impact | Mitigation |
|----|------|------------|--------|-----------|
| R-001 | AI ranking introduces bias and triggers legal/PR issues | Medium | High | Bias audit on training data; always-explainable recommendations; human override mandatory |
| R-002 | Job board APIs deprecate or change pricing | Medium | Medium | Abstract behind adapter layer; multi-board fallback; direct apply as baseline |
| R-003 | Calendar integration OAuth flows complex for enterprise customers | High | Medium | Ship Google Calendar first; Office 365 in 1.5; manual scheduling fallback always available |
| R-004 | GDPR compliance complexity across EU customers delays launch | Medium | High | Engage DPO consultant pre-launch; implement data consent from day one, not as retrofit |
| R-005 | AI generation latency exceeds UX targets under load | Low | Medium | Async generation with optimistic UI; streaming response where possible; cache common outputs |
| R-006 | Small team under-estimates complexity of multi-tenant data isolation | Medium | High | Row-level security in Postgres from the start; dedicated tenant schemas for enterprise tier |

### Key Assumptions

- A1: Target customers (50–2,000 employees) have at least one dedicated recruiter who will act as primary user
- A2: Most organizations have Google Workspace or Microsoft 365 as their calendar system
- A3: AI ranking accuracy of ≥ 75% top-5 precision is achievable with resume + JD matching alone (no behavioral data)
- A4: Customers are willing to connect their job board accounts via OAuth for publishing
- A5: GDPR consent obtained at application submission is sufficient for AI scoring during the process

### Open Questions

- Q1: Should candidate self-scheduling be opt-in (recruiter chooses) or always-on?
- Q2: What is the primary monetization model — per-seat, per-hire, or tiered by company size?
- Q3: Should the AI ranker be trained per-organization (cold-start problem) or on a global model?
- Q4: Is GDPR right-to-erasure scoped to PII only, or should application/scorecard history also be purged?
- Q5: Should Hiring Managers require a paid seat, or be included in recruiter seat count?

---

## 13. Glossary

| Term | Definition |
|------|-----------|
| ATS | Applicant Tracking System — software to manage recruiting pipelines |
| Pipeline | The sequence of stages a candidate passes through from application to hire |
| Stage | A discrete step in the hiring pipeline (e.g., Applied, Phone Screen, Interview) |
| Scorecard | A structured feedback form completed by an interviewer post-interview |
| JD | Job Description — the document describing a role's responsibilities and requirements |
| Shortlist | The subset of applicants selected for active review, typically AI-ranked |
| Hiring Manager | The person who will manage the successful hire; often a team lead or department head |
| Recruiter | HR professional responsible for sourcing, screening, and coordinating candidates |
| Debrief | Post-interview meeting (or async review) where panel members share scorecard results |
| RBAC | Role-Based Access Control — permission model tied to user roles |
| MVP | Minimum Viable Product — the smallest scope that delivers core value to early customers |
| MoSCoW | Prioritization framework: Must have, Should have, Could have, Won't have |
| RICE | Prioritization framework: Reach, Impact, Confidence, Effort |
| GDPR | General Data Protection Regulation — EU data privacy law |
| SSO | Single Sign-On — enterprise authentication via identity provider |
| PWA | Progressive Web App — web application with native-like mobile capabilities |
| p99 | 99th percentile — the latency value below which 99% of requests fall |
| WCAG | Web Content Accessibility Guidelines — international accessibility standard |

---

## 14. Appendix

### A. Competitive Analysis Highlights

| Feature | LTI | Greenhouse | Lever | Workday |
|---------|-----|-----------|-------|---------|
| AI JD Generation | ✅ | ❌ | Partial | ❌ |
| AI Candidate Ranking | ✅ | Partial | Partial | Partial |
| Real-Time Collaboration | ✅ | ❌ | ✅ | ❌ |
| Automated Scheduling | ✅ | Partial | Partial | ✅ |
| Mid-Market Pricing | ✅ | Partial | ✅ | ❌ |
| Multi-Board Publishing | ✅ | ✅ | ✅ | ✅ |
| Mobile Hiring Manager UX | ✅ | Partial | Partial | ❌ |

### B. Related Documents

- `LTI-RACC/docs/project-brief.md` — original product brief
- `LTI-RACC/UserStories-RACC.md` — supplementary user story notes
- `ai-specs/specs/base-standards.mdc` — project development standards
- `ai-specs/specs/documentation-standards.mdc` — documentation standards

### C. Market Context

- Global ATS market size (2025): ~USD 3.2B, growing at ~7% CAGR
- AI-augmented HR tech segment: ~18% CAGR
- Mid-market segment (50–2,000 employees): underserved by both SMB tools (too simple) and enterprise tools (too complex/expensive)
- Average time-to-hire in mid-market companies: 28–42 days (LTI target: < 20 days for customers)
