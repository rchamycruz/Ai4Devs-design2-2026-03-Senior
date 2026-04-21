# Product Backlog

This folder contains the product backlog and all User Stories generated from the PRD.

## Structure

- `backlog.md` — Backlog summary with Epics, prioritized story list, release plan, and dependency map
- `us-001.md`, `us-002.md`, ... — Individual User Story files with full details

## How to use

1. **Generate the backlog**: Run `/create-backlog-plan` with your PRD file path (or leave empty to use `ai-specs/specs/PRD.md`)
2. **Enrich stories**: Run `/enrich-us` on each story to add technical detail
3. **Push to platform**: Run `/push-backlog-plan jira` or `/push-backlog-plan github` to sync with your project management tool

## Naming Convention

User Stories follow the format `us-XXX.md` where XXX is a zero-padded sequential number (001, 002, 003...).
