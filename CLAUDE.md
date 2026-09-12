# TrackForge

Trello/Jira-style Kanban tracker built to cover 2026 .NET essentials. Full task breakdown lives in GitHub Issues (#1-#20) and `PLAN.md`.

## Architecture

- Clean Architecture: `src/TrackForge.Domain`, `src/TrackForge.Application`, `src/TrackForge.Infrastructure`, `src/TrackForge.Api`
- CQRS via MediatR — commands for writes, queries for reads. No generic repository.
- Domain: Workspace → Board → List → Card, with Label, Member, CardPosition (value object for ordering)
- Business rules (authorization checks, position math) live in Domain/Application, never in controllers
- .NET 10, C# 14, PostgreSQL via EF Core
- Frontend (from Task 018 onward): React + TypeScript (Vite), dnd-kit for drag-and-drop, SignalR client

## Conventions

- Commits: `Task 0XX: <title>`, referencing the GitHub issue number
- One feature branch per task, PR into `master` (this repo's default branch — not `main`)
- Minimal APIs, not controllers
- FluentValidation on all commands
- Global exception handling via `IExceptionHandler` → `ProblemDetails`
- Nullable reference types enabled

## Before opening a PR

1. `dotnet build` and `dotnet test` must both pass
2. New business logic gets a corresponding xUnit test (unit test for Domain/Application, integration test via `WebApplicationFactory` for API endpoints)
3. Commit message references the issue: `Task 0XX: <title> (#<issue-number>)`
4. PR description states what was implemented and how it was tested — no unexplained scope creep beyond the issue

## Task sequencing note

Testing and observability (Tasks 011, 013) are meant to be woven in from Task 001 onward, not bolted on at the end — write tests alongside each feature as you go, and wire Serilog/OpenTelemetry in early.

## What NOT to do

- Don't implement tasks out of order without checking dependencies (e.g. Task 006 depends on the CardPosition value object from Task 002)
- Don't introduce a new architectural pattern not listed above without flagging it in the PR description for review
- Don't touch `.github/workflows/` or `.claude/settings.json` as part of a feature task
