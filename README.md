# Road Incidents API (.NET 8) — Technical Test

REST API to register road incidents and query them by department and/or date range, supporting pagination.
Built with .NET 8 following Clean Architecture, DDD principles, CQRS, and Mediator pattern.

## Tech Stack
- .NET 8 (ASP.NET Core)
- Clean Architecture (Domain / Application / Infrastructure / API)
- CQRS + MediatR (commands for writes, queries for reads)
- EF Core (persistence)
- xUnit (unit tests)
- Swagger (OpenAPI)

## Architecture
This solution is structured as:

- `RoadIncidents.Domain`
  Domain model: entities, invariants, and (optional) value objects.
- `RoadIncidents.Application`
  Use cases (CQRS): commands/queries + handlers, DTOs, interfaces, validation.
- `RoadIncidents.Infrastructure`
  EF Core DbContext, repository implementations, migrations.
- `RoadIncidents.Api`
  REST endpoints, dependency injection, middleware (errors), Swagger.
- `RoadIncidents.Tests.Unit`
  Unit tests for handlers and domain rules.

Dependency rule: outer layers depend on inner layers only.

## How to run
### Prerequisites
- .NET SDK 8

### Run API
```bash
dotnet restore
dotnet run --project src/RoadIncidents.Api
```

Swagger:
- `https://localhost:<port>/swagger`

### Run tests
```bash
dotnet test
```

## Endpoints (planned)
### Create incident
- `POST /api/incidents`

### Query incidents (filters + pagination)
- `GET /api/incidents?department=...&startDate=...&endDate=...&pageNumber=1&pageSize=20`

Notes:
- `department`, `startDate`, `endDate` are optional and combinable.
- Pagination is always applied with defaults.

## Documentation
- Domain model: `docs/domain-model.md`
- ADRs: `docs/adr/`

## Decisions (ADRs)
See `docs/adr/README.md` for the decision log.

## What’s next
- Implement Domain model (RoadIncident aggregate)
- Add CQRS handlers (Create + Query)
- Add persistence (EF Core + migrations)
- Add unit tests (handlers + validation)
- Add error handling via ProblemDetails
