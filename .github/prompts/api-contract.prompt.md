---
description: Create or review OpenAPI contract for an Angular-consumed backend API
---

Using the approved forward specification:

1. Create/update the OpenAPI contract.
2. Define REST endpoints.
3. Define request models.
4. Define response models.
5. Define validation.
6. Define HTTP status codes.
7. Define error responses.
8. Define pagination/filtering/sorting where applicable.
9. Verify the contract is sufficient for Angular implementation.
10. Verify it does not expose persistence implementation details.

Do not implement Java.

Do not invent API fields.

If the specification does not contain enough information, create decision-required.md.

Return API_CONTRACT_STATUS.