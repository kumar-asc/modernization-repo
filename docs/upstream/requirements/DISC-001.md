# DISC-001 - Search Disclosure

## User Story

As a Disclosure user, I want to search disclosures using optional filters so that I can find relevant disclosure records without retrieving the entire dataset.

## Acceptance Criteria

### AC-01 - Search Endpoint

The system must expose:

GET /api/disclosures/v1/search

### AC-02 - Optional Filters

The API supports the following optional query parameters:

- disclosureId
- status
- type

### AC-03 - Pagination

The API supports:

- page
- size

Default:

page = 0
size = 20

Maximum size:

100

### AC-04 - Search Results

The API returns a paginated list of disclosures.

The response must contain:

- items
- page
- size
- totalElements
- totalPages

### AC-05 - No Results

If no disclosure matches the search criteria:

HTTP 200

The items collection must be empty.

### AC-06 - Invalid Request

Invalid pagination values must return:

HTTP 400

### AC-07 - Error Contract

Errors must contain:

- code
- message
- correlationId

### AC-08 - API Isolation

JPA/database entities must not be exposed directly through the REST API.

### AC-09 - Frontend Consumer

The API will be consumed by a separate Angular frontend application.

The OpenAPI contract must be sufficient for frontend implementation.