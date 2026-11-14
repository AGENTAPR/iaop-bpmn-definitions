# iaop-bpmn-definitions

BPMN and DMN process definitions.

## Purpose

iaop-bpmn-definitions is part of the **Insurance Agent Operating Platform (IAOP)**, an enterprise
insurance agent lifecycle platform.

## Bounded Context / Ownership

- **Bounded context:** Process Definitions
- **Owner:** AGENTAPR
- **Group:** architecture-docs

## Owned Database

N/A (no owned database)

Each service owns its persistence. No cross-service database access, no shared domain
entities, and no cross-database foreign keys.

## Technical Stack

BPMN 2.0, DMN

## Architecture Principles

- Domain-Driven Design (DDD) with explicit bounded contexts
- Hexagonal architecture (ports and adapters)
- Event-driven integration via versioned contracts (see iaop-event-contracts)
- Transactional outbox/inbox for reliable event publication
- PostgreSQL as the system of record where applicable
- Identity and access via Keycloak
- Workflow orchestration via Flowable BPM (see iaop-workflow-service)
- Observability via OpenTelemetry

## Responsibilities

- Versioned BPMN process definitions
- DMN decision tables
- Process model documentation

## Non-Responsibilities

- Process execution engine (iaop-workflow-service)
- Domain business logic
- Runtime state

## Integration

### Upstream (callers / producers toward this service)

- (none)

### Downstream (services this depends on)

- `iaop-workflow-service`
- `Domain services owning processes`

### Planned Integration Events

- (none planned yet)

Event schemas are governed by [iaop-event-contracts](https://github.com/AGENTAPR/iaop-event-contracts).

### Planned API Contracts

- (none yet)

API specifications are governed by [iaop-api-contracts](https://github.com/AGENTAPR/iaop-api-contracts).

## Related Repositories

- [iaop-architecture](https://github.com/AGENTAPR/iaop-architecture) - DDD strategic design, bounded context maps, ADRs, repository landscape
- [iaop-rust-common](https://github.com/AGENTAPR/iaop-rust-common) - Shared Rust technical utilities
- [iaop-test-kit](https://github.com/AGENTAPR/iaop-test-kit) - Shared test infrastructure

## Status

**INITIALIZED - NOT IMPLEMENTED**

This repository has been bootstrapped with baseline documentation and configuration only.
No business logic or service implementation exists yet.

## Development Conventions

- Default branch: `main`
- Development branch: `development` — all changes are committed and pushed here
- Squash merges preferred; merge commits and rebases disabled
- Pull requests required before merging into `main`
- Topics: iaop, insurance, insurance-agents, enterprise-architecture, bpmn, dmn, flowable, workflow, documentation
## Foundation implementation (2026-11)

- `processes/agent-onboarding.bpmn` — example executable BPMN 2.0 process (`iaop.onboarding.agent-onboarding`): screening → profile creation → agreement → activation
- Conventions: process IDs `iaop.<context>.<name>`; human tasks bound to Keycloak groups; service tasks via `##delegate` expressions
- `.github/workflows/main-ci.yml` — XML validation on `main` pushes only
