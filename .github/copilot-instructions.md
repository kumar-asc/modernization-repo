# Backend RPG-to-Java Modernization

## Purpose

This repository contains the Java backend implementation of an IBM RPG/Synon modernization program.

Discovery and backward engineering have already been completed by an upstream team.

The backend team is responsible for forward engineering and implementation.

The forward engineering process is:

Upstream Artifacts
-> Forward Specification
-> API Contract
-> Implementation
-> Tests
-> Architecture Review

---

# Upstream Artifacts

The following directories contain approved inputs from the upstream discovery/backward-engineering team:

- docs/upstream/domain-model/
- docs/upstream/modularization/
- docs/upstream/requirements/
- docs/upstream/rpg-mapping/

These artifacts are READ-ONLY from the backend team's perspective.

Do not modify upstream artifacts.

If an inconsistency or missing information is found:

1. Identify the issue.
2. Document it under the current feature's forward-engineering directory.
3. Mark the implementation/specification as BLOCKED when necessary.
4. Do not invent business behavior.

---

# Services

The backend consists of:

1. disclosure-service
2. workaction-service
3. core-shared-library

---

# disclosure-service

Owns the Disclosure domain.

Expected responsibilities include:

- Disclosure APIs
- Disclosure business logic
- Disclosure persistence
- Disclosure validation
- Disclosure integrations
- Disclosure-specific exceptions
- Disclosure-specific resilience policies

---

# workaction-service

Owns the WorkAction domain.

Expected responsibilities include:

- WorkAction APIs
- WorkAction business logic
- WorkAction persistence
- WorkAction validation
- WorkAction integrations
- WorkAction-specific exceptions
- WorkAction-specific resilience policies

---

# core-shared-library

Contains only genuinely shared technical infrastructure.

Current responsibilities:

- logging
- correlation ID support
- messaging abstractions/infrastructure
- common technical utilities where explicitly approved

Do NOT put the following into core-shared-library:

- business logic
- domain entities
- service-specific DTOs
- service-specific exceptions
- service-specific repositories
- service-specific clients
- service-specific configuration
- service-specific resilience policies

---

# Service Dependencies

Allowed:

disclosure-service
-> core-shared-library

workaction-service
-> core-shared-library

Not allowed:

core-shared-library
-> disclosure-service

core-shared-library
-> workaction-service

disclosure-service
-> workaction-service implementation classes

workaction-service
-> disclosure-service implementation classes

Cross-service communication must use an approved REST or messaging contract.

---

# API Standards

Backend APIs are consumed by a separate Angular frontend team.

The OpenAPI/API contract is the contract between frontend and backend.

Example:

GET /api/disclosures/v1/search

API contracts must be defined and reviewed before implementation.

Do not expose JPA entities directly through REST APIs.

Use request/response DTOs.

Use appropriate HTTP methods and status codes.

Define:

- request contract
- response contract
- validation
- error contract
- pagination
- filtering
- sorting
- correlation requirements

Do not invent API fields that are not supported by approved requirements or design.

---

# REST Integration

For synchronous service-to-service communication:

- use an explicit API contract
- define timeout
- define retry behavior
- define error handling
- define idempotency requirements
- propagate correlation ID

Do not directly call another service's Java classes.

---

# Messaging

For asynchronous communication:

- use the approved messaging infrastructure
- use explicit message contracts
- include message ID
- include correlation ID
- support idempotent consumers
- define retry behavior
- define dead-letter behavior

Do not invent message schemas.

---

# Resilience

Resilience policies belong to the service that owns the integration.

Do NOT put service-specific resilience implementations into core-shared-library.

For every external integration explicitly consider:

- timeout
- retry
- backoff
- circuit breaker
- fallback
- idempotency

Do not retry non-idempotent operations blindly.

Do not retry permanent business errors.

---

# Exceptions

Each service owns its own exception hierarchy.

Each service owns its REST exception handling.

Business exceptions must not be placed in core-shared-library.

Do not expose stack traces or internal infrastructure details through APIs.

---

# Logging

Use structured logging.

Propagate correlation IDs across:

- REST
- REST client calls
- messaging

Never log:

- passwords
- tokens
- secrets
- private keys
- sensitive customer information

---

# Java Standards

Use the project's approved Java/Spring versions and dependencies.

Prefer:

- constructor injection
- immutable DTOs where appropriate
- records where appropriate
- clear domain naming
- small cohesive classes
- explicit dependencies
- meaningful exception types

Avoid:

- God classes
- unnecessary abstractions
- static mutable state
- speculative frameworks
- unnecessary design patterns

---

# RPG Modernization

Do not perform line-by-line RPG translation.

Preserve approved business behavior.

Use RPG/Synon artifacts as behavioral evidence.

The target implementation should represent the approved business/domain behavior using appropriate Java/Spring patterns.

Never invent business rules.

If behavior is unclear:

STOP -> DOCUMENT -> REQUEST DECISION

Do not:

GUESS -> IMPLEMENT

---

# Scope Control

When implementing a story:

Only modify files required by the approved implementation scope.

Do not:

- refactor unrelated code
- modify unrelated services
- change approved APIs
- modify upstream documents
- introduce dependencies without approval
- change architecture silently

---

# Testing

Every implemented requirement must have appropriate automated test coverage.

Test:

- happy path
- validation
- business rules
- persistence behavior
- integration failures
- resilience behavior where applicable
- messaging behavior where applicable

Tests must verify behavior rather than implementation details.

---

# AI Behavior

Before implementation:

1. Read the relevant upstream artifacts.
2. Read the forward-engineering package.
3. Understand the approved scope.
4. Identify missing information.
5. Stop if a critical architectural/business decision is missing.

Never silently invent:

- API fields
- database fields
- business rules
- integration behavior
- resilience policies
- error semantics

---

# Final Response

After completing a task, report:

1. Summary
2. Files changed
3. Requirements implemented
4. Tests added
5. Tests executed
6. Assumptions
7. Known gaps
8. Decision-required items