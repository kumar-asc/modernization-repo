---
description: Implement an approved backend modernization story
---

Implement the current story using the approved forward-engineering package.

Before changing code:

1. Read copilot-instructions.md.
2. Read the feature README.
3. Read forward-spec.md.
4. Read api-contract.yaml.
5. Read persistence-spec.md.
6. Read integration-spec.md.
7. Read error-contract.md.
8. Read resilience-spec.md.
9. Read implementation-scope.md.
10. Read test-spec.md.
11. Check decision-required.md.

If the story is blocked, do not implement.

Implement only approved scope.

Do not:

- invent business rules
- change APIs
- modify upstream artifacts
- refactor unrelated code
- introduce unapproved dependencies
- modify unrelated services
- put business logic into core-shared-library

After implementation:

1. Run tests.
2. Fix implementation issues.
3. Do not weaken tests.
4. Report all assumptions and gaps.

Return the standard implementation report.