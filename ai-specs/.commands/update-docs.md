Use `ai-specs/specs/documentation-standards.mdc` to update whatever documentation is needed according to the changes made.

# Extended Scope

Beyond the standard technical documentation, this command must also review and update the following areas when changes affect them:

## Diagrams (`ai-specs/diagrams/`)

If the `ai-specs/diagrams/` folder exists, review and update all diagram files to reflect the current state of the project:

1. **Entity-Relationship Diagram** (`entity-relationship.md`):
   - Must stay in sync with `ai-specs/specs/data-model.md` and any Prisma schema changes
   - Add/remove/rename entities and relationships as needed

2. **Sequence Diagrams** (`sequence-diagrams.md`):
   - Must reflect current API endpoints from `ai-specs/specs/api-spec.yml`
   - Update flows when controller/service logic changes

3. **C4 Architecture Diagrams** (`c4-architecture.md`):
   - Update containers when new services, databases, or external integrations are added
   - Update components when internal architecture changes

4. **Use Case Diagrams** (`use-cases.md`):
   - Add new use cases when PRD features or user stories are added
   - Update actor relationships when roles change

5. **Lean Canvas** (`lean-canvas.md`):
   - Update when product strategy, target users, or business model changes

## Backlog (`ai-specs/backlog/`)

If the `ai-specs/backlog/` folder exists:
- Update `backlog.md` summary if new stories were added or priorities changed
- Update individual `us-XXX.md` files if acceptance criteria or technical details were affected by code changes

## PRD (`ai-specs/specs/PRD.md`)

If the PRD exists, verify it still reflects the current product scope. Flag sections that may be outdated but do not modify the PRD without explicit user approval.

## Other project `.md` files

Scan the workspace for any `.md` files related to the project (README.md, CHANGELOG.md, CONTRIBUTING.md, etc.) and update them if recent changes affect their content.

# Process

1. Run `git diff` (or review the recent changes provided) to identify what changed
2. For each change, determine which documentation files are affected using the mapping above
3. Update each affected file, maintaining English language and existing formatting conventions
4. Verify Mermaid diagram syntax is valid after any diagram updates
5. Report a summary of all files updated and what changed in each