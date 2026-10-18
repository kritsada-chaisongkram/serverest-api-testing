# ServeRest API Testing Portfolio

> **Work in progress** | Current milestone: **User Management — Manual API Testing**

## Project Overview

This portfolio demonstrates a structured approach to testing REST APIs using **ServeRest**, a practice e-commerce API. The project begins with manual API test design and execution in Postman and will be extended with automated API tests and CI execution as development progresses.

The goal is to demonstrate practical QA skills: understanding API behavior, designing positive and negative tests, checking expected versus actual results, managing test data, and documenting reproducible evidence.

**Current progress (18 October 2026):** Four User Management test cases have been manually executed and passed. The remaining modules and automation activities are planned, not yet completed.

## System Under Test

| Item | Detail |
| --- | --- |
| Application | ServeRest — e-commerce practice REST API |
| Base URL | `https://serverest.dev` |
| API documentation | [ServeRest API documentation](https://serverest.dev/) |
| Source project | [ServeRest official GitHub repository](https://github.com/ServeRest/ServeRest) |
| Test environment | ServeRest public online environment |
| Current testing tool | Postman |

ServeRest is maintained by an external open-source project. The API and its documentation are **not** developed or owned by this portfolio's author. Test scenarios, execution records, and evidence in this repository are portfolio work.

Test expectations are informed by the published API documentation and observed behavior. Any additional test objectives are portfolio-derived; they should not be represented as official business acceptance criteria.

## Test Scope and Progress

| Module / Activity | Scope | Status |
| --- | --- | --- |
| User Management | Create users, reject duplicate email, validate required email, retrieve a user by ID | **Completed — 4/4 manual tests passed** |
| Authentication | Login and authorization scenarios | Planned |
| Products | Product API scenarios | Planned |
| Cart | Cart API scenarios | Planned |
| API Automation | Postman assertions, reusable variables, request chaining, selected data-driven tests | Planned |
| CI/CD | Newman execution and GitHub Actions reporting | Planned |

**Scope note:** “Completed” refers only to the four documented User Management manual test cases, not to all possible User Management behaviors or the entire API.

## Testing Approach

The current manual testing work includes:

- **Positive testing:** Validate a successful request with valid input.
- **Negative testing:** Validate API rejection of duplicate and incomplete data.
- **Response validation:** Check HTTP status codes, response fields, and error messages.
- **Data consistency:** Confirm that a retrieved user's details match the user created for the test.
- **Test evidence:** Capture the request configuration and observed response for each execution.

Test cases and expected results are documented separately from actual execution results. A new execution record is used for a retest rather than overwriting an earlier result.

## User Management — Manual Test Results

- **Execution date:** 18 October 2026
- **Environment:** ServeRest public API
- **Execution method:** Manual API requests in Postman

| Test Case ID | Scenario | Method | Endpoint | Expected HTTP Status | Result |
| --- | --- | --- | --- | --- | --- |
| `TC-USER-001` | Create a user with valid data | `POST` | `/usuarios` | `201` | **PASS** |
| `TC-USER-002` | Reject an email already registered | `POST` | `/usuarios` | `400` | **PASS** |
| `TC-USER-003` | Reject a request missing the required `email` field | `POST` | `/usuarios` | `400` | **PASS** |
| `TC-USER-004` | Retrieve the newly created user by ID | `GET` | `/usuarios/{id}` | `200` | **PASS** |

### Observed Results

- **TC-USER-001:** The API returned `201 Created`, a success message (`Cadastro realizado com sucesso`), and a generated user `_id`.
- **TC-USER-002:** The API returned `400 Bad Request` with the message `Este email já está sendo usado` for the duplicate email.
- **TC-USER-003:** The API returned `400 Bad Request` with `email é obrigatório` when the `email` field was omitted.
- **TC-USER-004:** The API returned `200 OK` and the retrieved user data matched the user created during testing.

The quoted Portuguese messages above reflect the observed API responses; they have not been rewritten as English response payloads.

### Execution Summary

| Metric | Count |
| --- | ---: |
| Executed test cases | 4 |
| Passed | 4 |
| Failed | 0 |
| Confirmed defects | 0 |

These results describe the recorded manual executions only. They do not imply complete API coverage or an automated test run.

## Test Documentation and Evidence

Manual test design and execution results are managed in **one Excel workbook with two worksheets**:

1. **Test Cases:** Scenarios, requirements, preconditions, request data, steps, and expected results.
2. **Test Execution:** Per-run actual results, status, execution date, evidence reference, and retest history.

For the GitHub milestone, place the workbook at `test-documentation/ServeRest_API_Test_Cases_Final.xlsx` (or update this path to match its final filename).

For each of the four completed manual test cases, evidence is organized into two screenshots: `01_REQUEST` (request configuration) and `02_RESPONSE` (observed HTTP response). The intended repository paths are:

| Test Case | Request Evidence | Response Evidence |
| --- | --- | --- |
| `TC-USER-001` | `evidence/manual-api/user-management/TC-USER-001_01_REQUEST.png` | `evidence/manual-api/user-management/TC-USER-001_02_RESPONSE.png` |
| `TC-USER-002` | `evidence/manual-api/user-management/TC-USER-002_01_REQUEST.png` | `evidence/manual-api/user-management/TC-USER-002_02_RESPONSE.png` |
| `TC-USER-003` | `evidence/manual-api/user-management/TC-USER-003_01_REQUEST.png` | `evidence/manual-api/user-management/TC-USER-003_02_RESPONSE.png` |
| `TC-USER-004` | `evidence/manual-api/user-management/TC-USER-004_01_REQUEST.png` | `evidence/manual-api/user-management/TC-USER-004_02_RESPONSE.png` |

**Publishing note:** These paths are local evidence references for the current milestone. After the files are committed to GitHub, links can be added to the Excel `Evidence` field and to this README. No GitHub-hosted evidence links are claimed yet.

## Environment Notes and Limitations

- The public ServeRest environment is shared, and its data is cleared daily according to the project's documentation. Tests must not rely on records remaining available between separate sessions.
- User creation and retrieval scenarios depend on valid test data and the ID returned during the current run. Future automation will create its own required data and reuse the generated ID rather than depend on a hard-coded record.
- Error messages are returned in Portuguese. Assertions and reports should preserve the actual response text when checking exact values.
- The current results are limited to the four listed manual scenarios. Authentication, Products, Cart, automation, and CI/CD have not yet been reported as completed.
- Only disposable, purpose-created demo credentials should be used in public test artifacts. Real passwords, tokens, and secrets must not be published.

## Next Milestones

1. Publish the current User Management Excel workbook and request/response evidence on GitHub.
2. Design and execute selected Authentication, Products, and Cart API scenarios.
3. Automate appropriate scenarios with Postman assertions, variables, request chaining, and a focused data-driven test.
4. Run the collection with Newman and add GitHub Actions execution with downloadable test reports.
5. Update the overall test summary, limitations, evidence links, and README as each milestone is completed.

## References and Attribution

- [ServeRest — API Documentation](https://serverest.dev/)
- [ServeRest — Official Source Repository](https://github.com/ServeRest/ServeRest)

This is an independent QA learning and portfolio project. It is not an official ServeRest test suite or a claim of production certification.
