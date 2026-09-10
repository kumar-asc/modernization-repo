# Disclosure Domain Model

Version: 1.0

Status: APPROVED

## Disclosure

The Disclosure domain represents a disclosure record.

### Attributes

| Attribute | Type | Description |
|---|---|---|
| disclosureId | String | Unique identifier |
| status | String | Current disclosure status |
| type | String | Disclosure type |
| title | String | Disclosure title |
| createdDate | DateTime | Creation timestamp |
| updatedDate | DateTime | Last update timestamp |

## Searchable Attributes

The following attributes are searchable:

- disclosureId
- status
- type

## Business Rules

1. A Disclosure must have a unique disclosureId.
2. status represents the current lifecycle state.
3. type represents the classification of the disclosure.

## Important

This document represents the approved domain model.

The backend implementation must not introduce additional business fields unless required by an approved requirement.