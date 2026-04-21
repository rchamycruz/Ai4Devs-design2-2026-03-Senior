# Consolidado del Proyecto LTI — AI4Devs Design 2026-03 Senior

**Autor**: RACC (Rodrigo Chamy Cruz)  
**Fecha**: 2026-04-21  
**Repositorio**: [rchamycruz/Ai4Devs-design2-2026-03-Senior](https://github.com/rchamycruz/Ai4Devs-design2-2026-03-Senior)

---

## 1. Prompts Utilizados en esta Sesión

A continuación se listan los prompts utilizados durante la sesión de trabajo, en orden cronológico:

### Prompt 1 — Crear comando `create-prd` y agente Product Manager
> Analiza la carpeta .commands, crea un nuevo comando llamado "create-prd" para crear un archivo PRD.md con instrucciones, así como lo hace por ejemplo el archivo plan-backend-ticket.md. A la vez crea un agente en la carpeta .agents que sea un experto para crear PRD, que podria ser un Product Manager and Business Analyst. PRD = Product Requirements Document tomado como ejemplo los otros agentes que se encuentran en la carpeta .agents.

**Resultado**: Se creó el comando `create-prd.md` y el agente `product-manager-ba.md`. Fue efectivo porque reutilizó una técnica ya conocida con agentes y comandos, ahorrando explicaciones.

### Prompt 2 — Corregir argumento del comando create-prd
> El comando create PRD debe recibir como argumento el nombre del archivo o la ruta del archivo que contiene el contexto del proyecto. Corrige eso.

**Resultado**: Se corrigió el comando para recibir `$ARGUMENTS` como ruta del archivo de contexto del proyecto.

### Prompt 3 — Crear comandos de backlog y push-backlog
> Analiza la carpeta .commands, crea un nuevo comando llamado "create-backlog-plan" para crear un archivo backlog.md con instrucciones, así como lo hace por ejemplo el archivo plan-backend-ticket.md. A la vez crea un agente en la carpeta .agents que sea un experto para crear Backlogs de software, que podria ser un Product Manager and Business Analyst, tomando como ejemplo los otros agentes que se encuentran en la carpeta .agents. El create-backlog-plan debe recibir como argumento un archivo con el PRD o si viene vacío el argumento tomar el archivo PRD.md de la solución. Por último, un comando nuevo que debes generar es push-backlog-plan.md, este comando enviará a Jira o Github Project (se recibe como parámetro) y crear el backlog con las Épicas e Historias de usuario enriquecidas ya por el comando enrich-us.md. Para finalizar, debes crear una carpeta para ir dejando todo el backlog y las historias de usuario creadas (separadas por archivo con formato us-001 incremental).

**Resultado**: Se crearon `create-backlog-plan.md`, `push-backlog-plan.md`, el agente `backlog-planner.md` y la carpeta `ai-specs/backlog/`.

### Prompt 4 — Agregar BDD y estimación al backlog
> Al create-backlog-plan.md agrégale que debe indicar criterio de aceptación en base a Behavior-Driven Development y Estima el esfuerzo de los tickets de trabajo usando la metodología (fibonacci, poker, tallas de camiseta) y unidades.

**Resultado**: Se enriqueció el comando con criterios de aceptación BDD (Gherkin) y triple estimación (Fibonacci, Planning Poker, T-Shirt).

### Prompt 5 — Agregar casos de uso a cada User Story
> También que en cada User Story creada agregue el Caso de uso al que corresponde, y de ser posible, con su diagrama.

**Resultado**: Cada User Story incluye referencia al caso de uso del PRD con diagrama Mermaid.

### Prompt 6 — Crear comando de diagramas y agente diagram-architect
> Analiza la carpeta .commands, crea un nuevo comando llamado "create-diagrams.md" para crear una carpeta llamada "diagrams" y dentro de ella crear diagramas de secuencia, de casos de uso, de lean canvas, C4, entidad relación en archivos separados. También crea un agente que sea experto para cada uno de los casos. El comando "update-docs" también debe actualizar los diagramas y cualquier otro archivo .md que tenga relación con el proyecto.

**Resultado**: Se creó `create-diagrams.md`, el agente `diagram-architect.md`, y se actualizó `update-docs.md` para incluir diagramas.

### Prompt 7 — Vincular backlog con diagramas
> Tanto create-backlog-plan como push-backlog-plan deben considerar leer los diagramas creados si existen.

**Resultado**: Ambos comandos ahora leen `ai-specs/diagrams/` para enriquecer el contexto.

### Prompt 8 — Generar sub tasks para US-001 en GitHub
> Genera tickets de trabajo (sub task) para la Historia de Usuario US-001 en Github.

**Resultado**: Se generaron 12 sub tasks (#22–#33) para US-001 en GitHub Issues.

### Prompt 9 — Estimar esfuerzo de sub task #22
> A la Sub task [US-001][BE][DB] #22 de la historia de Usuario US-001 en Github Estima el esfuerzo usando la metodología (fibonacci, poker, tallas de camiseta) y unidades.

**Resultado**: Se estimó el esfuerzo del issue #22 y se actualizó en GitHub.

### Prompt 10 — Generar consolidado (este documento)
> Añade al archivo UserStories-RACC.md un consolidado con: Prompts utilizados en esta sesión, estructura de carpetas del backlog, .commands, .agents, diagramas, y contenido de épicas, historias y sub tasks de GitHub.

**Resultado**: Este documento.

---

## 2. Estructura de Carpetas del Backlog

```
ai-specs/
├── backlog/
│   ├── README.md
│   ├── backlog.md
│   ├── us-001.md
│   ├── us-002.md
│   ├── us-003.md
│   ├── us-004.md
│   ├── us-005.md
│   ├── us-006.md
│   ├── us-007.md
│   ├── us-008.md
│   ├── us-009.md
│   ├── us-010.md
│   ├── us-011.md
│   └── us-012.md
├── diagrams/
│   ├── c4-architecture.md
│   ├── entity-relationship.md
│   ├── lean-canvas.md
│   ├── sequence-diagrams.md
│   └── use-cases.md
├── specs/
│   ├── api-spec.yml
│   ├── backend-standards.mdc
│   ├── base-standards.mdc
│   ├── data-model.md
│   ├── development_guide.md
│   ├── documentation-standards.mdc
│   ├── frontend-standards.mdc
│   └── PRD.md
├── .commands/
│   ├── commit.md
│   ├── create-backlog-plan.md
│   ├── create-diagrams.md
│   ├── create-prd.md
│   ├── develop-backend.md
│   ├── develop-frontend.md
│   ├── enrich-us.md
│   ├── explain.md
│   ├── meta-prompt.md
│   ├── plan-backend-ticket.md
│   ├── plan-frontend-ticket.md
│   ├── push-backlog-plan.md
│   └── update-docs.md
└── .agents/
    ├── backend-developer.md
    ├── backlog-planner.md
    ├── diagram-architect.md
    ├── frontend-developer.md
    ├── product-manager-ba.md
    └── product-strategy-analyst.md
```

### Contenido de `backlog/README.md`

```markdown
# Product Backlog

This folder contains the product backlog and all User Stories generated from the PRD.

## Structure
- `backlog.md` — Backlog summary with Epics, prioritized story list, release plan, and dependency map
- `us-001.md`, `us-002.md`, ... — Individual User Story files with full details

## How to use
1. **Generate the backlog**: Run `/create-backlog-plan` with your PRD file path
2. **Enrich stories**: Run `/enrich-us` on each story to add technical detail
3. **Push to platform**: Run `/push-backlog-plan jira` or `/push-backlog-plan github`

## Naming Convention
User Stories follow the format `us-XXX.md` where XXX is a zero-padded sequential number (001, 002, 003...).
```

### Contenido de `backlog/backlog.md` (Resumen)

- **Producto**: LTI — Next-Generation Applicant Tracking System
- **Total Stories**: 12
- **Total Story Points**: 107
- **Método de priorización**: RICE Scoring
- **Método de estimación**: Fibonacci + Planning Poker + T-Shirt Sizing
- **MVP Scope**: 8 stories Must Have (73 puntos), ~8 sprints de 2 semanas
- **Release 1.5**: 4 stories Should Have (34 puntos), ~4 sprints
- **9 Épicas**: E-01 a E-09

---

## 3. Comandos (.commands) Creados

| Comando | Descripción |
|---------|-------------|
| **`create-prd.md`** | Genera un Product Requirements Document (PRD) completo a partir de un archivo de contexto del proyecto. Recibe como argumento la ruta del archivo fuente. |
| **`create-backlog-plan.md`** | Genera un backlog completo con Épicas y User Stories a partir de un PRD. Incluye criterios de aceptación BDD (Gherkin), triple estimación (Fibonacci/Poker/T-Shirt), y caso de uso asociado a cada historia. |
| **`create-diagrams.md`** | Genera una carpeta `diagrams/` con 5 tipos de diagramas: Lean Canvas, Casos de Uso, C4 Architecture, Entidad-Relación y Secuencia. |
| **`push-backlog-plan.md`** | Publica el backlog enriquecido en Jira o GitHub Projects. Recibe como parámetro `jira` o `github`. Crea Épicas e Issues con labels, milestones y relaciones. |
| **`enrich-us.md`** | Enriquece una User Story con detalle técnico suficiente para implementación autónoma por un desarrollador. Agrega criterios de aceptación BDD, arquitectura DDD, API spec, tests y NFRs. |
| **`plan-backend-ticket.md`** | Genera un plan de implementación paso a paso para un ticket backend siguiendo DDD/Clean Architecture. |
| **`plan-frontend-ticket.md`** | Genera un plan de implementación paso a paso para un ticket frontend siguiendo arquitectura de componentes React. |
| **`develop-backend.md`** | Implementa un ticket backend: crea branch, codifica, testea, hace commit y crea PR. |
| **`develop-frontend.md`** | Implementa un ticket frontend desde Figma: genera componentes React, estilos y estructura siguiendo Atomic Design. |
| **`commit.md`** | Genera un commit comprensivo con PR. Puede acotar por ticket ID o hacer commit de todos los cambios. |
| **`update-docs.md`** | Actualiza toda la documentación afectada por cambios recientes: diagramas, backlog, PRD y otros archivos .md del proyecto. |
| **`explain.md`** | Facilita el aprendizaje de conceptos detrás de una pregunta. Optimiza para adquisición de habilidades, no para respuestas rápidas. |
| **`meta-prompt.md`** | Toma un prompt y lo reestructura aplicando mejores prácticas de prompt engineering. |

---

## 4. Agentes (.agents) Creados

| Agente | Modelo | Descripción |
|--------|--------|-------------|
| **`product-manager-ba.md`** | opus | Product Manager y Business Analyst experto en crear PRDs, definir user stories, construir backlogs, diseñar data models y hacer análisis de negocio. Combina pensamiento estratégico de PM con rigor de BA. |
| **`backlog-planner.md`** | opus | Especialista en creación, descomposición y priorización de backlogs. Experto en INVEST, RICE, MoSCoW, BDD, estimación Fibonacci/T-Shirt y gestión de dependencias. |
| **`diagram-architect.md`** | sonnet | Arquitecto de software y especialista en documentación visual. Experto en producir diagramas Mermaid: secuencia, casos de uso, Lean Canvas, C4 y entidad-relación. |
| **`backend-developer.md`** | sonnet | Arquitecto TypeScript backend especializado en DDD con capas (Domain, Application, Presentation, Infrastructure), Prisma ORM, Express/Fastify y PostgreSQL. |
| **`frontend-developer.md`** | sonnet | Desarrollador React experto en arquitectura de componentes, service layer, React Router, React Bootstrap y TypeScript. |
| **`product-strategy-analyst.md`** | opus | Estratega de producto experto en ideación, análisis de mercado, definición de personas, propuesta de valor (Jobs-to-be-Done, Value Proposition Canvas) y estrategia de MVP. |

---

## 5. Diagramas Creados

### 5.1 Lean Canvas — `ai-specs/diagrams/lean-canvas.md`

**Descripción**: Captura el modelo de negocio de LTI en una sola página: problemas de equipos HR, soluciones AI-first, propuesta de valor única, segmentos de clientes, métricas clave, canales, estructura de costos y flujos de ingresos.

**Contenido principal**:
- **Problema**: Admin overload (60-70% del tiempo del recruiter), falta de colaboración en tiempo real, mala experiencia del candidato
- **Solución**: AI co-pilot (generación JD, ranking CV, detección de bias), workspace colaborativo en tiempo real, automatización completa del pipeline
- **UVP**: "Hire better, faster — with AI as your co-pilot and real-time collaboration built in"
- **Ventaja competitiva**: AI ranking model fine-tuned con datos de recruiting + feedback loop
- **Segmentos**: Mid-market HR teams (50-2,000 empleados), tech firms en crecimiento, Hiring Managers
- **Revenue**: SaaS por requisiciones abiertas (Starter/Growth/Enterprise)

### 5.2 Casos de Uso — `ai-specs/diagrams/use-cases.md`

**Descripción**: Mapea todos los actores del sistema LTI (Recruiter, Hiring Manager, Interviewer, HR Director, Candidate, AI System) con sus 19 casos de uso, mostrando relaciones include/extend y conexiones con sistemas externos (Job Boards, Calendar, Assessment Providers, Notifications).

**Casos de uso principales**: Create & Edit Job (UC1), AI Generate Job Description (UC2), Approve Job Post (UC3), Publish Job to Channels (UC4), Receive Applications (UC5), Parse & Rank Candidates - AI (UC6), Review Candidate Shortlist (UC7), Schedule Interview (UC12), Submit Scorecard (UC14), View Analytics Dashboard (UC17).

### 5.3 Arquitectura C4 — `ai-specs/diagrams/c4-architecture.md`

**Descripción**: Describe la arquitectura del sistema LTI en tres niveles de abstracción C4:

- **Level 1 - System Context**: LTI como caja negra interactuando con 5 tipos de usuarios y 7 sistemas externos (Job Boards, Calendar, Assessment Providers, Claude API, SendGrid, Twilio, Auth0)
- **Level 2 - Container**: 7 contenedores desplegables: Web App (React 19), Backend API (Node.js/Fastify), AI Service (Python/FastAPI), Job Queue (BullMQ/Redis), PostgreSQL 17, Redis 7, File Storage (S3)
- **Level 3 - Component (Backend API)**: 12 componentes internos incluyendo API Router, Auth & RBAC Middleware, Jobs Module, Pipeline Module, Scheduling Module, Collaboration Module, Notification Module, Analytics Module, AI Gateway, Webhook Handler, Domain Models y Repositories

### 5.4 Entidad-Relación — `ai-specs/diagrams/entity-relationship.md`

**Descripción**: Cubre las 11 entidades core del modelo de datos LTI centrado en `Application` como registro operacional que conecta `Candidate` con `Job`. Multi-tenancy anclado en `Organization`.

**Entidades**: Organization, User, Job, JobPublication, Candidate, Application, ApplicationNote, Interview, InterviewerAssignment, Scorecard, Assessment, Notification.

### 5.5 Diagramas de Secuencia — `ai-specs/diagrams/sequence-diagrams.md`

**Descripción**: Cubre los 4 flujos de negocio principales del PRD:

1. **User Authentication Flow**: JWT con access tokens de 15 min y refresh token rotation
2. **Job Creation & AI-Assisted Publication**: Drafting con AI JD generation, aprobación del Hiring Manager, publicación multi-canal
3. **Candidate Screening & AI Ranking**: Envío de aplicación, CV parsing asíncrono + AI ranking via Claude API, colaboración recruiter/manager
4. **Interview Scheduling & Hire Decision**: Detección de disponibilidad, self-scheduling del candidato, scorecards, debrief y decisión final

---

## 6. Épicas, Historias de Usuario y Sub Tasks de GitHub

### 6.1 Épicas (2 de 9)

#### Épica #2 — E-02: Job Management & AI-Assisted Creation

- **Estado**: Open
- **Objetivo de Negocio**: B1 (reducir time-to-hire), B4 (reducir tiempo admin)
- **Descripción**: AI-drafted job descriptions con detección de bias en tiempo real, workflow de aprobación del Hiring Manager in-platform, y publicación multi-canal a LinkedIn, Indeed, Glassdoor y career page.
- **Contexto de Arquitectura**: Jobs Module + AI Gateway (Claude API para generación JD) + BullMQ publish workers + job board adapters
- **Stories**: US-001 (8 pts), US-002 (13 pts)
- **Total**: 21 story points | Must Have | MVP Release 1.0
- **Labels**: `epic`, `priority:must-have`, `mvp`

#### Épica #5 — E-05: Interview Scheduling & Scorecards

- **Estado**: Open
- **Objetivo de Negocio**: B1 (reducir time-to-hire), B2 (NPS)
- **Descripción**: Detección automatizada de disponibilidad del panel via Google Calendar, self-scheduling del candidato con URLs autenticadas por token, creación de eventos de calendario para todos los asistentes, recordatorios T-24h/T-1h, envío de scorecards estructurados y vista de debrief agregada.
- **Contexto de Arquitectura**: Scheduling Module + Google Calendar API + BullMQ delayed reminder tasks. Entidades: Interview, InterviewerAssignment, Scorecard
- **Stories**: US-005 (13 pts), US-006 (5 pts)
- **Total**: 18 story points | Must Have | MVP Release 1.0
- **Labels**: `epic`, `priority:must-have`, `mvp`

---

### 6.2 Historias de Usuario (Issue #12 y #22)

#### Issue #12 — US-002: Multi-Channel Job Publishing

- **Estado**: Open
- **Epic**: #2 E-02 Job Management
- **Points**: 13 | **T-Shirt**: XL | **RICE**: 8.4 | **Priority**: Must Have
- **Labels**: `user-story`, `priority:must-have`, `mvp`, `points:13`

**Story**: As a Recruiter, I want to publish a job to multiple boards in one click, so that I reach more candidates without duplicating effort.

**Acceptance Criteria (BDD)**:
```gherkin
Feature: Multi-Channel Job Publishing

  Scenario 1: Recruiter publishes to two channels successfully
    Given a job exists with status "approved"
      And the organization has connected LinkedIn and Indeed via OAuth
    When a recruiter sends POST /api/v1/jobs/{id}/publish { channels: ["linkedin", "indeed"] }
    Then the API responds with 202 Accepted
      And two BullMQ tasks are enqueued (one per channel)
      And within 60 seconds both job_publications records have status "live"

  Scenario 2: Partial failure — one channel fails, the other succeeds
    Given a job exists with status "approved"
      And the Indeed API is returning 503 Service Unavailable
    When the publish job tasks are processed by workers
    Then the LinkedIn job_publication record has status "live"
      And the Indeed job_publication record has status "failed"
      And the failed task is retried with exponential backoff (3 attempts max)

  Scenario 3: Source tagging on inbound application webhook
    Given a job is live on LinkedIn with external_id "li-ext-123"
    When a candidate applies via LinkedIn and the webhook is received
    Then the application record is created with source = "linkedin"

  Scenario 4: Recruiter attempts to publish a job not yet approved
    Given a job exists with status "draft"
    When a recruiter sends POST /api/v1/jobs/{id}/publish
    Then the API responds with 422 Unprocessable Entity

  Scenario 5: Career page channel always available without OAuth
    When a recruiter publishes to the "career_page" channel
    Then the job is immediately published to the company career page
      And no external API call is made

  Scenario 6: Organization has not connected a job board
    Given an organization has not connected LinkedIn via OAuth
    When a recruiter opens the channel selector
    Then LinkedIn appears disabled with badge "Not connected"
```

**Arquitectura DDD**:
```
src/
  domain/models/JobPublication.ts
  domain/repositories/IJobPublicationRepository.ts
  application/services/jobPublishService.ts
  infrastructure/repositories/JobPublicationRepository.ts
  infrastructure/encryption/tokenEncryption.ts
  integrations/linkedin.adapter.ts, indeed.adapter.ts, glassdoor.adapter.ts, careerPage.adapter.ts
  workers/publishJob.worker.ts
  presentation/controllers/jobPublish.controller.ts, webhook.controller.ts
```

**Estimación**: Fibonacci 13 | Poker 13 | T-Shirt XL | 26–32 horas
**Dependencias**: Blocked by #11 (US-001)

---

#### Issue #22 — [US-001][BE][DB] Create jobs table migration

- **Estado**: Open
- **Parent Story**: #11 — US-001: AI Job Description Generator
- **Tipo**: Sub Task
- **Labels**: `task`, `backend`, `database`, `mvp`

**Descripción**: Create the database migration for the `jobs` table.

**Archivo**: `src/db/migrations/002_jobs_table.sql`

**Schema**:
```sql
CREATE TABLE jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  organization_id UUID NOT NULL REFERENCES organizations(id),
  created_by UUID NOT NULL REFERENCES users(id),
  hiring_manager_id UUID REFERENCES users(id),
  title VARCHAR(255) NOT NULL,
  description_html TEXT,
  status VARCHAR(50) NOT NULL DEFAULT 'draft' CHECK (status IN ('draft','approved','open','closed')),
  location VARCHAR(255),
  salary_min INTEGER,
  salary_max INTEGER,
  tags TEXT[],
  published_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_jobs_org_status ON jobs(organization_id, status);
```

**Acceptance**:
- [ ] Migration runs without errors on a clean DB
- [ ] Migration is reversible (DOWN script included)
- [ ] Index on `(organization_id, status)` created

---

### 6.3 Sub Tasks de la Historia de Usuario US-001 (Parent de #22)

#### Sub Task #25 — [US-001][AI] AI Service: JD generation + bias detection endpoint

- **Estado**: Open
- **Parent Story**: #11 — US-001: AI Job Description Generator
- **Labels**: `task`, `backend`, `ai`, `mvp`

**Descripción**: Implementar el endpoint Python/FastAPI que llama a la Claude API para generar una descripción de puesto estructurada y ejecutar detección de bias en la salida.

**Archivo**: `src/ai_service/routers/generate_jd.py`

**Endpoint**: `POST http://ai-service:8001/generate-jd`

**Request**:
```json
{ "title": "Senior Backend Engineer", "level": "Senior" }
```

**Response**:
```json
{
  "draft_html": "<h2>Summary</h2>...",
  "bias_flags": [
    { "phrase": "young and energetic", "reason": "age-biased language", "suggestion": "collaborative and dynamic" }
  ]
}
```

**Implementation Notes**:
- Usar Claude API (modelo `claude-sonnet-4-6`) con structured system prompt
- JD sections: Summary, Responsibilities, Requirements, Nice-to-haves
- Bias detection contra curated phrase list (age, gender, nationality bias patterns)
- Target latency: p50 < 3s, p99 < 8s

**Acceptance**:
- [ ] Returns structured HTML with all 4 sections
- [ ] Bias flags correctly identify at least 10 known biased phrases (golden dataset)
- [ ] Returns 503 with actionable message when Claude API is unavailable
- [ ] Unit tests with mocked Claude API responses

---

#### Sub Task #26 — [US-001][BE] AI Gateway Service — facade to AI microservice

- **Estado**: Open
- **Parent Story**: #11 — US-001: AI Job Description Generator
- **Labels**: `task`, `backend`, `mvp`

**Descripción**: Crear un facade TypeScript que llama al AI Service Python sincrónicamente para generación de JD. Es el único punto de integración entre el backend Node.js y el microservicio AI.

**Archivo**: `src/modules/ai/ai-gateway.service.ts`

**Interface**:
```typescript
interface JDGenerationResult {
  draft_html: string;
  bias_flags: Array<{ phrase: string; reason: string; suggestion: string }>;
}

class AIGatewayService {
  async generateJobDescription(title: string, level: string): Promise<JDGenerationResult>;
}
```

**Implementation Notes**:
- HTTP call a `http://ai-service:8001/generate-jd` via `axios` o `undici`
- Hard timeout: 10s (configurable via env `AI_SERVICE_TIMEOUT_MS`)
- On timeout o 5xx: throw `AIServiceUnavailableError` (controller → 503)
- Base URL desde env `AI_SERVICE_BASE_URL`

**Acceptance**:
- [ ] Successful call returns typed `JDGenerationResult`
- [ ] Timeout throws `AIServiceUnavailableError`
- [ ] 5xx from AI Service also throws `AIServiceUnavailableError`
- [ ] Unit tests with mocked HTTP (nock or msw)
