# Project Plan: Kanban/Issue Tracker (working name: TrackForge)

A Trello/Jira-style board app, chosen because a real-time, multi-entity domain is one of the few project shapes that naturally forces you through nearly every 2026 .NET essential in one coherent codebase — not a mockup, not a CRUD demo.

Domain: Workspaces → Boards → Lists → Cards, with members, labels, comments, due dates, and drag-and-drop reordering.

Structure follows the usual convention: numbered tasks (see GitHub Issues #1-#20), one feature branch per task, PR into `main`, commit messages as `Task 0XX: <title>`.

See the repo's GitHub Issues for the full task breakdown, grouped by label:
- `backend-core` (001-006): solution scaffold, domain model, EF Core + PostgreSQL/CQRS, JWT auth, Boards/Lists API, Cards API
- `differentiator` (007-010): SignalR real-time updates, HybridCache + Redis, Hangfire background jobs, Elasticsearch search
- `production-hygiene` (011-014): testing (xUnit/WebApplicationFactory/Testcontainers), OpenAPI/Scalar docs, Serilog + OpenTelemetry observability, Polly resilience
- `infra-delivery` (015-019): containerization, .NET Aspire AppHost, GitHub Actions CI/CD, React/TS frontend, Azure Container Apps deployment
- `stretch` (020): notification microservice split-out with Native AOT + outbox pattern

## Sequencing note

Testing (011) and observability (013) are usually treated as afterthoughts. Don't do that here — write tests alongside 005/006 and wire in Serilog/OpenTelemetry from 001. It reads better in the commit history and is genuinely less work than retrofitting.
