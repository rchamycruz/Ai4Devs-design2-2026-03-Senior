# Sequence Diagrams: LTI — Next-Generation Applicant Tracking System

These diagrams cover the three primary business flows from the PRD use cases, plus authentication. Each diagram traces the full interaction across actors, frontend, API, services, and external systems.

---

## 1. User Authentication Flow

JWT-based authentication with short-lived access tokens and refresh token rotation. SSO via SAML/OIDC is an alternative path for enterprise customers handled by Auth0/Clerk.

```mermaid
sequenceDiagram
    actor User
    participant Frontend as Frontend (React SPA)
    participant API as API Gateway (Fastify)
    participant AuthSvc as Auth Service (Auth0/Clerk)
    participant DB as PostgreSQL

    User->>Frontend: Enter email + password
    Frontend->>API: POST /api/v1/auth/login { email, password }
    API->>AuthSvc: validateCredentials(email, password)
    AuthSvc->>DB: SELECT user WHERE email = ? AND is_active = true
    DB-->>AuthSvc: User record

    alt Valid credentials
        AuthSvc-->>API: { userId, role, organizationId }
        API->>API: Sign JWT access_token (15 min) + refresh_token (7 days)
        API-->>Frontend: 200 OK { access_token, refresh_token, user }
        Frontend->>Frontend: Store tokens in memory / HttpOnly cookie
        Frontend-->>User: Redirect to Dashboard
    else Invalid credentials
        AuthSvc-->>API: AuthenticationError
        API-->>Frontend: 401 Unauthorized { error: "invalid_credentials" }
        Frontend-->>User: Show error message
    end
```

---

## 2. Job Creation & AI-Assisted Publication Flow (Use Case 1)

Covers job drafting with AI JD generation, hiring manager approval via in-platform collaboration, and multi-channel job board publishing.

```mermaid
sequenceDiagram
    actor Recruiter
    actor HiringManager as Hiring Manager
    participant Frontend as Frontend (React SPA)
    participant API as API Gateway
    participant JobsModule as Jobs Module (Node.js)
    participant Queue as BullMQ Queue
    participant AISvc as AI Service (Python / Claude API)
    participant DB as PostgreSQL
    participant NotifSvc as Notification Service
    participant JobBoard as Job Board API (LinkedIn/Indeed)

    Recruiter->>Frontend: Click "New Job", enter role title + level
    Frontend->>API: POST /api/v1/jobs/ai/generate-description { title, level }
    API->>AISvc: generateJobDescription(title, level)
    AISvc->>AISvc: Call Claude API with role prompt + bias detection
    AISvc-->>API: { draft_html, bias_flags[] }
    API-->>Frontend: 200 OK { draft_html, bias_flags }
    Frontend-->>Recruiter: Show AI draft in split-pane editor with inline bias warnings

    Recruiter->>Frontend: Edit description, fill requirements, click "Save Draft"
    Frontend->>API: POST /api/v1/jobs { title, description_html, requirements... }
    API->>JobsModule: createJob(payload)
    JobsModule->>DB: INSERT INTO jobs (status='draft', ...)
    DB-->>JobsModule: job { id }
    JobsModule->>NotifSvc: notifyHiringManager(job.hiring_manager_id, job.id)
    NotifSvc-->>HiringManager: In-app + email notification: "Job pending your approval"
    API-->>Frontend: 201 Created { job }
    Frontend-->>Recruiter: Job saved, awaiting manager approval

    HiringManager->>Frontend: Open job review, leave comment or click "Approve"
    Frontend->>API: POST /api/v1/applications/{jobId}/notes { content: "Approved!" }
    API->>DB: INSERT INTO application_notes ...
    API->>NotifSvc: notifyRecruiter(job.created_by, "Job approved")
    NotifSvc-->>Recruiter: In-app + email: "Hiring Manager approved your job post"

    Recruiter->>Frontend: Select channels (LinkedIn, Indeed, Career Page), click "Publish"
    Frontend->>API: POST /api/v1/jobs/{id}/publish { channels: ["linkedin","indeed","career_page"] }
    API->>JobsModule: publishJob(jobId, channels)

    loop For each channel
        JobsModule->>Queue: enqueue PublishJobTask { jobId, channel }
    end

    Queue->>JobBoard: POST job via LinkedIn Jobs API
    JobBoard-->>Queue: { external_id }
    Queue->>DB: INSERT INTO job_publications (channel, external_id, status='live')

    Queue->>DB: UPDATE jobs SET status='open', published_at=NOW()
    API-->>Frontend: 200 OK { publications[] }
    Frontend-->>Recruiter: Job is live on 3 channels
```

---

## 3. Candidate Screening & AI Ranking Flow (Use Case 2)

Covers application submission, asynchronous CV parsing + AI ranking, and recruiter/manager collaboration on the shortlist.

```mermaid
sequenceDiagram
    actor Candidate
    actor Recruiter
    actor HiringManager as Hiring Manager
    participant CareersPage as Career Page (Public)
    participant API as API Gateway
    participant PipelineModule as Pipeline Module
    participant Queue as BullMQ Queue
    participant AISvc as AI Service (Python / Claude API)
    participant S3 as File Storage (S3)
    participant DB as PostgreSQL
    participant NotifSvc as Notification Service
    participant WS as WebSocket Service

    Candidate->>CareersPage: Fill application form, attach CV
    CareersPage->>API: POST /api/v1/jobs/{jobId}/applications { candidate, resume_file }
    API->>S3: Upload resume → resume_url
    S3-->>API: resume_url
    API->>PipelineModule: createApplication({ candidate, job_id, resume_url, source })
    PipelineModule->>DB: INSERT INTO candidates (if new) + INSERT INTO applications (stage='applied')
    DB-->>PipelineModule: { application_id, candidate_id }
    PipelineModule->>Queue: enqueue ParseAndRankTask { application_id, resume_url, job_id }
    API-->>CareersPage: 201 Created { application_id }
    CareersPage-->>Candidate: "Application submitted! We'll be in touch."

    Note over Queue,AISvc: Async processing (target: < 60s)

    Queue->>AISvc: parseAndRank({ resume_url, job_id })
    AISvc->>S3: Fetch resume file
    S3-->>AISvc: PDF/DOCX content
    AISvc->>AISvc: Extract structured data (skills, exp, education)
    AISvc->>DB: SELECT job requirements WHERE job_id = ?
    DB-->>AISvc: Job requirements
    AISvc->>AISvc: Call Claude API: score candidate vs. requirements
    AISvc->>DB: UPDATE applications SET ai_score=?, ai_score_rationale=?
    AISvc-->>Queue: Done
    Queue->>WS: broadcast({ event: "application.ranked", application_id, ai_score })
    WS-->>Recruiter: Real-time update: new ranked application in pipeline board

    Recruiter->>API: GET /api/v1/jobs/{jobId}/applications?sort=ai_score&limit=20
    API->>DB: SELECT applications ORDER BY ai_score DESC
    DB-->>API: Ranked applications[]
    API-->>Recruiter: Shortlist with AI scores + rationale badges

    Recruiter->>API: POST /api/v1/applications/{id}/notes { content: "Strong Python background, share with Marco" }
    API->>DB: INSERT INTO application_notes
    API->>NotifSvc: notify(hiring_manager_id, "@mention in application")
    NotifSvc-->>HiringManager: Email + in-app: "Recruiter shared a candidate with you"

    HiringManager->>API: GET /api/v1/applications/{id}
    API-->>HiringManager: Full candidate profile (CV, AI score, notes)
    HiringManager->>API: POST /api/v1/applications/{id}/notes { content: "Looks great, move to phone screen" }
    API->>DB: INSERT INTO application_notes
    API->>NotifSvc: notifyRecruiter("Manager responded")
    NotifSvc-->>Recruiter: Notification

    Recruiter->>API: PATCH /api/v1/applications/{id}/stage { stage: "phone_screen" }
    API->>DB: UPDATE applications SET stage='phone_screen'
    API->>NotifSvc: sendCandidateNotification(candidate_id, "phone_screen", template)
    NotifSvc-->>Candidate: Email/SMS: "Congratulations! You've advanced to the Phone Screen stage."
```

---

## 4. Interview Scheduling & Hire Decision Flow (Use Case 3)

Covers automated panel availability check, candidate self-scheduling, scorecard collection, debrief, and final hire decision.

```mermaid
sequenceDiagram
    actor Recruiter
    actor Candidate
    actor Interviewer1 as Interviewer (Lead)
    actor Interviewer2 as Interviewer (Panelist)
    actor HiringManager as Hiring Manager
    participant API as API Gateway
    participant SchedulingModule as Scheduling Module
    participant CalendarAPI as Calendar API (Google/Outlook)
    participant DB as PostgreSQL
    participant NotifSvc as Notification Service (SendGrid/Twilio)

    Recruiter->>API: POST /api/v1/applications/{id}/interviews { panel: [userId1, userId2], type: "panel" }
    API->>SchedulingModule: proposeSlots(panelUserIds)
    SchedulingModule->>CalendarAPI: GET free/busy for userId1, userId2 (next 7 days)
    CalendarAPI-->>SchedulingModule: Availability windows[]
    SchedulingModule->>SchedulingModule: Find overlapping 60-min slots (≥ 3)
    SchedulingModule->>DB: INSERT INTO interviews (status='pending', calendar_event_ids=null)
    DB-->>SchedulingModule: { interview_id }
    SchedulingModule-->>API: { interview_id, proposed_slots[3] }
    API->>NotifSvc: sendSchedulingLink(candidate_email, { interview_id, slots, token })
    NotifSvc-->>Candidate: Email with self-scheduling link

    Candidate->>API: GET /api/v1/candidates/schedule/{token}
    API-->>Candidate: Scheduling page with 3 available slots

    Candidate->>API: POST /api/v1/candidates/schedule/{token} { selected_slot: "2026-05-03T14:00:00Z" }
    API->>SchedulingModule: confirmSlot(interview_id, selected_slot)
    SchedulingModule->>CalendarAPI: Create calendar event (Recruiter + Interviewer1 + Interviewer2 + Candidate)
    CalendarAPI-->>SchedulingModule: { event_ids{} }
    SchedulingModule->>DB: UPDATE interviews SET scheduled_at=?, status='scheduled', calendar_event_ids=?
    SchedulingModule->>NotifSvc: scheduleReminders(interview_id, ["-24h", "-1h"])
    SchedulingModule-->>API: Confirmed
    API-->>Candidate: 200 OK — "Interview confirmed for May 3, 2:00 PM"
    API->>NotifSvc: notifyPanel(interviewers[], "Interview scheduled with Candidate")
    NotifSvc-->>Recruiter: Calendar invite + notification
    NotifSvc-->>Interviewer1: Calendar invite + notification
    NotifSvc-->>Interviewer2: Calendar invite + notification

    Note over NotifSvc: Auto-reminders fire at T-24h and T-1h

    Note over Interviewer1,Interviewer2: Interview takes place

    Interviewer1->>API: POST /api/v1/interviews/{id}/scorecards { ratings, overall_rating: "strong_yes", hire_recommendation: true }
    API->>DB: INSERT INTO scorecards
    Interviewer2->>API: POST /api/v1/interviews/{id}/scorecards { ratings, overall_rating: "yes", hire_recommendation: true }
    API->>DB: INSERT INTO scorecards
    API->>DB: UPDATE interviews SET status='completed'

    Recruiter->>API: GET /api/v1/interviews/{id}/scorecards
    API->>DB: SELECT scorecards WHERE interview_id = ?
    DB-->>API: Aggregated scores + individual ratings
    API-->>Recruiter: Debrief view with avg score + individual feedback

    HiringManager->>API: GET /api/v1/interviews/{id}/scorecards
    API-->>HiringManager: Same debrief view

    HiringManager->>API: POST /api/v1/applications/{id}/notes { content: "Strong hire — approved!" }
    API->>DB: INSERT INTO application_notes

    Recruiter->>API: PATCH /api/v1/applications/{id}/stage { stage: "offer" }
    API->>DB: UPDATE applications SET stage='offer'
    API->>NotifSvc: sendCandidateNotification(candidate_id, "offer_pending", template)
    NotifSvc-->>Candidate: Email: "Great news — we'd like to extend an offer!"

    Recruiter->>API: PATCH /api/v1/applications/{id}/stage { stage: "hired" }
    API->>DB: UPDATE applications SET stage='hired'
    API->>DB: UPDATE jobs SET status='closed' (if all positions filled)
    API-->>Recruiter: Pipeline closed — hire event logged
```

---

## 5. HR Analytics Dashboard Load Flow (Use Case 17)

Covers an HR Director loading the analytics dashboard with server-side aggregation, caching, and filtered results.

```mermaid
sequenceDiagram
    actor HRDirector as HR Director
    participant Frontend as Frontend (React SPA)
    participant API as API Gateway
    participant AuthMiddleware as RBAC Middleware
    participant AnalyticsModule as Analytics Module
    participant Redis as Redis Cache
    participant DB as PostgreSQL (Read Replica)

    HRDirector->>Frontend: Navigate to Analytics
    Frontend->>API: GET /api/v1/analytics/funnel?team=engineering&range=90d
    API->>AuthMiddleware: verifyRole(user.role, ["hr_director","admin"])
    AuthMiddleware-->>API: Authorized

    API->>Redis: GET analytics:funnel:org123:engineering:90d
    alt Cache hit (TTL: 15 min)
        Redis-->>API: Cached funnel data
        API-->>Frontend: 200 OK { funnel, cached: true }
    else Cache miss
        Redis-->>API: null
        API->>AnalyticsModule: computeFunnel(org_id, filters)
        AnalyticsModule->>DB: SELECT stage, COUNT(*) FROM applications WHERE ... GROUP BY stage
        DB-->>AnalyticsModule: Stage counts[]
        AnalyticsModule->>DB: SELECT AVG(hired_at - applied_at) FROM applications WHERE stage='hired'
        DB-->>AnalyticsModule: avg_time_to_hire
        AnalyticsModule-->>API: { funnel, time_to_hire, source_breakdown }
        API->>Redis: SET analytics:funnel:org123:engineering:90d EX 900
        API-->>Frontend: 200 OK { funnel, time_to_hire, source_breakdown, cached: false }
    end

    Frontend-->>HRDirector: Render dashboard cards + funnel chart + source pie chart

    HRDirector->>Frontend: Click "Export CSV"
    Frontend->>API: GET /api/v1/analytics/funnel?format=csv&team=engineering&range=90d
    API->>AnalyticsModule: generateCSV(org_id, filters)
    AnalyticsModule-->>API: CSV file stream
    API-->>Frontend: 200 OK Content-Type: text/csv
    Frontend-->>HRDirector: Download file
```

---

## Notes & Assumptions

- All sequence diagrams assume TLS 1.3 in transit for all HTTP calls; not annotated on every arrow for readability.
- The async CV parsing flow (Flow 3) uses BullMQ + WebSocket push to avoid polling. If WebSocket connection is unavailable, the frontend falls back to polling `GET /applications/{id}` every 10s.
- Calendar API calls in Flow 4 assume OAuth tokens are pre-authorized during organization setup (Settings → Integrations). Expired OAuth tokens trigger a re-authorization prompt to the Recruiter.
- Reminder notifications in Flow 4 are queued as delayed BullMQ jobs at the time the interview is confirmed, not at the reminder fire time. This avoids cron dependencies.
- Analytics cache TTL of 15 minutes (900s) is a starting assumption; this should be tunable per organization size and dashboard refresh expectations.
- PATCH `/applications/{id}/stage` is the single endpoint driving all pipeline stage transitions; it internally validates allowed transitions (e.g., cannot jump from `applied` directly to `hired`) using a state machine in the Pipeline Module.
