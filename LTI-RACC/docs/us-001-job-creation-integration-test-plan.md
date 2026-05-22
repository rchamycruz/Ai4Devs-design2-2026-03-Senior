# US-001 Integration Test Plan

## Goal
Validate the end-to-end happy path for AI-assisted job creation, from description generation to draft save and hiring manager notification.

## Target Test File
`src/tests/integration/us-001-job-creation.spec.ts`

## Scope
### Flow 1: Full AI-assisted creation
1. `POST /api/v1/jobs/ai/generate-description` with `title` and `level`
2. `POST /api/v1/jobs` with `title`, `description_html`, `hiring_manager_id`, and related fields
3. Assert notification record creation for the hiring manager
4. Assert email task enqueued in BullMQ through the mailer spy

### Flow 2: Manual save with bias detection
1. `POST /api/v1/jobs` with `description_html` containing biased language
2. Assert the API returns `bias_flags` for the detected phrase

### Flow 3: AI service unavailable
1. Stub the AI service to return `503`
2. `POST /api/v1/jobs/ai/generate-description`
3. Assert no job record is created and no notification is enqueued

## Test Setup
- Use the test database with isolated transactions per test
- Stub the AI service with `nock` or `msw`
- Replace SendGrid/email dispatch with an in-memory spy
- Use deterministic fixtures for users, organizations, and hiring managers

## Assertions
- `draft_html` includes the four required sections
- `bias_flags` is returned and persisted when applicable
- Saved jobs default to `draft`
- Notification is created for the correct hiring manager
- Email task is queued exactly once
- AI failures return a graceful `503` response

## Acceptance Criteria
- All three flows pass consistently in CI
- No shared test data leaks between tests
- The suite completes in under 10 seconds

## Risks
- Queue jobs may become flaky if async workers are not mocked
- Shared fixtures may leak state without transaction rollback
- External AI/email dependencies must never be called directly in the test
