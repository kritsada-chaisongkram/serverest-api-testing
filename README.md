# ServeRest API Testing Portfolio

> **Work in Progress** | Completed Manual Milestones: **User Management and Authentication**

## Project Overview

This portfolio demonstrates a structured approach to REST API testing using **ServeRest**, a practice e-commerce API.

The project focuses on manual API test design and execution using Postman, with plans to expand into API automation and CI/CD.

The goal is to demonstrate practical QA skills, including:

- Understanding API requirements and expected behavior
- Designing positive and negative test scenarios
- Validating HTTP status codes and response data
- Managing test data and dependencies
- Recording actual results and execution evidence
- Identifying and documenting defects
- Developing maintainable API automation tests

**Current Progress (20 October 2026):** Eight documented manual API test cases across User Management and Authentication have been executed. All eight passed their defined behavior checks. The precise HTTP error contract for one Authentication negative test remains unverified independently. Products, Cart, automation, and CI/CD are planned.

## System Under Test

| Item | Description |
|---|---|
| Application | ServeRest |
| Application Type | E-commerce REST API |
| Base URL | `https://serverest.dev` |
| API Documentation | [ServeRest API Documentation](https://serverest.dev/) |
| Official Source | [ServeRest GitHub](https://github.com/ServeRest/ServeRest) |
| Environment | Public API environment |
| Current Testing Tool | Postman |
| Documentation | Microsoft Excel |
| Version Control | Git and GitHub |

ServeRest is an external open-source project. This repository contains independently developed QA portfolio work and is not an official ServeRest test suite.

Test expectations are based on published API documentation and observed behavior. Portfolio-derived test objectives are not represented as official business acceptance criteria.

---

## Test Scope and Progress

| Module / Activity | Scope | Status |
|---|---|---|
| User Management | Create user, duplicate email, missing email, retrieve user | Completed — 4/4 manual tests passed |
| Authentication | Valid login, invalid password, unregistered email, missing email field | Completed — 4/4 behavioral checks passed; one error-response contract detail requires clarification |
| Products | Product API scenarios | Planned |
| Cart | Cart API scenarios | Planned |
| API Automation | Postman assertions, variables, request chaining, data-driven testing | Planned |
| CI/CD | Newman and GitHub Actions | Planned |

**Scope Note:** Completed means the eight documented manual scenarios passed their defined behavior checks; this does not indicate complete coverage of User Management, Authentication, or authorization rules.

---

## Testing Approach

### Manual API Testing

Manual API tests are designed and executed using Postman.

The testing approach includes:

- **Positive Testing:** Verify successful API behavior with valid requests.
- **Negative Testing:** Verify appropriate error responses for invalid or incomplete requests.
- **Status Code Validation:** Compare actual HTTP status codes against expected results.
- **Response Validation:** Verify required response fields, values, and messages.
- **Data Consistency:** Confirm retrieved information matches previously created test data.
- **Test Evidence:** Capture request configuration and actual API responses.

Test design and execution results are maintained separately in the Excel workbook.

### API Automation — Planned

The automation phase is planned to cover selected risk-based scenarios using:

- Postman JavaScript assertions
- Collection and environment variables
- Request chaining
- Dynamic test data
- Data-driven testing
- JSON schema validation
- Newman CLI
- GitHub Actions CI
- Execution reports and artifacts

Automation tests have not yet been implemented or executed as part of this portfolio.

---

## User Management — Manual Test Results

- **Execution Date:** 18 October 2026
- **Environment:** ServeRest Public API
- **Execution Method:** Manual API requests using Postman

### Test Case Summary

| Test Case ID | Test Scenario | Method | Endpoint | Expected Status | Actual Result |
|---|---|---|---|---|---|
| TC-USER-001 | Create a user with valid data | POST | `/usuarios` | 201 | PASS |
| TC-USER-002 | Reject duplicate email registration | POST | `/usuarios` | 400 | PASS |
| TC-USER-003 | Reject user creation without email | POST | `/usuarios` | 400 | PASS |
| TC-USER-004 | Retrieve an existing user by ID | GET | `/usuarios/{id}` | 200 | PASS |

### Observed Results

**TC-USER-001 — Create User**

- HTTP Status: `201 Created`
- Success Message: `Cadastro realizado com sucesso`
- A unique user `_id` was returned.
- Result: **PASS**

**TC-USER-002 — Duplicate Email**

- HTTP Status: `400 Bad Request`
- Error Message: `Este email já está sendo usado`
- Duplicate email registration was rejected.
- Result: **PASS**

**TC-USER-003 — Missing Email**

- HTTP Status: `400 Bad Request`
- Error Response: `email é obrigatório`
- The request was rejected when the required `email` field was omitted.
- Result: **PASS**

**TC-USER-004 — Get User by ID**

- HTTP Status: `200 OK`
- The requested user was retrieved.
- Returned user information matched the user created during testing.
- Result: **PASS**

The Portuguese messages above reflect observed ServeRest API responses.

### Test Execution Summary

| Metric | Result |
|---|---:|
| Total Executed | 4 |
| Passed | 4 |
| Failed | 0 |
| Confirmed Defects | 0 |
| Recorded Pass Rate | 100% |

**Result:** All four documented User Management manual scenarios passed.

These results apply only to the recorded manual executions and do not represent complete API coverage or an automated test run.

---

## Authentication — Manual Test Results

- **Execution Dates:** 18–20 October 2026
- **Environment:** ServeRest Public API
- **Execution Method:** Manual API requests in Postman
- **Endpoint Under Test:** `POST /login`

### Test Case Summary

| Test Case ID | Test Scenario | Observed HTTP Status | Behavioral Result |
|---|---|---|---|
| TC-AUTH-001 | Login with valid registered credentials | `200 OK` | PASS |
| TC-AUTH-002 | Reject login with an incorrect password | `401 Unauthorized` | PASS |
| TC-AUTH-003 | Reject login with an unregistered email | `401 Unauthorized` | PASS |
| TC-AUTH-004 | Reject login when the `email` field is omitted | `400 Bad Request` | PASS — behavior; exact error-response contract not independently confirmed |

### Observed Results

**TC-AUTH-001 — Valid Login**

- The API returned `200 OK` with `message: Login realizado com sucesso`.
- The response included an `authorization` value using the Bearer scheme.
- The public screenshot **redacts the token value**.

**TC-AUTH-002 — Invalid Password**

- A registered email was used with an incorrect password.
- The API returned `401 Unauthorized` and `message: Email e/ou senha inválidos`.
- The response did not contain an authorization token.
- A successful login using valid credentials was used to confirm the registered-user precondition.

**TC-AUTH-003 — Unregistered Email**

- Before the login attempt, `GET /usuarios?email=...` returned `200 OK` with `quantidade: 0` and `usuarios: []` for the email under test.
- The API returned `401 Unauthorized` and `message: Email e/ou senha inválidos` for the attempted login.
- No authorization token was returned.

**TC-AUTH-004 — Missing Email Field**

- The login request included `password` but **omitted** the `email` property entirely (not an empty string).
- The API rejected the request with `400 Bad Request` and `email: email é obrigatório`.
- No authorization token was returned.
- **Contract limitation:** The rejection behavior passed; the exact required HTTP status and error-message wording have not been independently confirmed against a published acceptance criterion. The observed response is not treated as proof of the intended contract.

### Authentication Test Data Setup and Precondition Check

Before the valid-login test, a disposable user was created through `POST /usuarios`; user creation returned `201 Created` with a generated `_id`. This was a **test setup step**, not an additional Authentication test case. Registered credentials were reused for the relevant login scenarios.

For the unregistered-email scenario, a separate `GET /usuarios?email=...` request confirmed no matching user was found. This was a **precondition check**, not an additional test case.

See the SETUP and CHECK evidence links below. ServeRest public test data may change or reset, so subsequent executions should verify prerequisites again.

### Authentication Execution Summary

| Metric | Count |
|---|---:|
| Executed Authentication cases | 4 |
| Passed behavioral checks | 4 |
| Failed behavioral checks | 0 |
| Error-response contract details awaiting confirmation | 1 |

**Overall manual progress:** 8 recorded test cases across User Management and Authentication, with 8 behavioral PASS results and no confirmed defects in those executed scenarios. This does not imply full API coverage.

---

## Test Documentation

The project maintains manual test documentation in a single Excel workbook containing two worksheets.

### 1. Test Cases

Contains:

- Test Case ID
- Test Scenario
- Requirements and Preconditions
- HTTP Method and Endpoint
- Request Data
- Test Steps
- Expected Results

### 2. Test Execution

Contains:

- Test Case ID
- Execution Information
- Actual Results
- PASS / FAIL Status
- Execution Date
- Evidence References
- Retest Information

**Excel Workbook:**

[View ServeRest API Test Cases and Execution Results](test-documentation/ServeRest_API_Test_Cases.xlsx)

---

## Manual Test Evidence

Each completed manual test case includes request and response screenshots. The Authentication module also includes separate setup/precondition evidence:

- **SETUP:** A successful test-user registration (`201 Created`).
- **CHECK:** Confirmation that the email used for TC-AUTH-003 was not registered.

- **Request Evidence:** Postman request configuration and test data.
- **Response Evidence:** Actual HTTP status and API response.

### User Management Evidence

#### TC-USER-001 — Create User

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-001_CREATE_USER_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-001_CREATE_USER_RESPONSE.png)

#### TC-USER-002 — Duplicate Email

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-002_DUPLICATE_EMAIL_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-002_DUPLICATE_EMAIL_RESPONSE.png)

#### TC-USER-003 — Missing Email

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-003_MISSING_EMAIL_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-003_MISSING_EMAIL_RESPONSE.png)

#### TC-USER-004 — Get User by ID

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-004_GET_USER_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-004_GET_USER_RESPONSE.png)

These eight User Management evidence files are retained from the previous milestone.

### Authentication Evidence

**Test Data Preparation (SETUP)**

- [SETUP — Create User Request](evidence/manual-api/authentication/SETUP_CREATE_AUTH_USER_REQUEST.png)
- [SETUP — Create User Response](evidence/manual-api/authentication/SETUP_CREATE_AUTH_USER_RESPONSE.png)

**Precondition Validation (CHECK)**

- [CHECK — Unregistered Email Result](evidence/manual-api/authentication/CHECK_UNREGISTERED_EMAIL_RESPONSE.png)

**TC-AUTH-001 — Valid Login**

- [Request Screenshot](evidence/manual-api/authentication/TC-AUTH-001_VALID_LOGIN_REQUEST.png)
- [Response Screenshot — Bearer Token Redacted](evidence/manual-api/authentication/TC-AUTH-001_VALID_LOGIN_RESPONSE.png)

**TC-AUTH-002 — Invalid Password**

- [Request Screenshot](evidence/manual-api/authentication/TC-AUTH-002_INVALID_PASSWORD_REQUEST.png)
- [Response Screenshot](evidence/manual-api/authentication/TC-AUTH-002_INVALID_PASSWORD_RESPONSE.png)

**TC-AUTH-003 — Unregistered Email**

- [Request Screenshot](evidence/manual-api/authentication/TC-AUTH-003_UNREGISTERED_EMAIL_REQUEST.png)
- [Response Screenshot](evidence/manual-api/authentication/TC-AUTH-003_UNREGISTERED_EMAIL_RESPONSE.png)

**TC-AUTH-004 — Missing Email Field**

- [Request Screenshot](evidence/manual-api/authentication/TC-AUTH-004_MISSING_EMAIL_REQUEST.png)
- [Response Screenshot](evidence/manual-api/authentication/TC-AUTH-004_MISSING_EMAIL_RESPONSE.png)

There are **11 Authentication evidence screenshots**: 2 setup, 1 precondition check, and 8 test execution screenshots. The Excel workbook holds the detailed test cases and recorded execution results. These links will resolve on GitHub after the Authentication milestone files are committed and pushed.

---

## Repository Structure

```text
serverest-api-testing/
├── .gitignore
├── README.md
├── test-documentation/
│   └── ServeRest_API_Test_Cases.xlsx
└── evidence/
    └── manual-api/
        ├── user-management/
        │   ├── TC-USER-001_CREATE_USER_REQUEST.png
        │   ├── TC-USER-001_CREATE_USER_RESPONSE.png
        │   ├── TC-USER-002_DUPLICATE_EMAIL_REQUEST.png
        │   ├── TC-USER-002_DUPLICATE_EMAIL_RESPONSE.png
        │   ├── TC-USER-003_MISSING_EMAIL_REQUEST.png
        │   ├── TC-USER-003_MISSING_EMAIL_RESPONSE.png
        │   ├── TC-USER-004_GET_USER_REQUEST.png
        │   └── TC-USER-004_GET_USER_RESPONSE.png
        └── authentication/
            ├── SETUP_CREATE_AUTH_USER_REQUEST.png
            ├── SETUP_CREATE_AUTH_USER_RESPONSE.png
            ├── CHECK_UNREGISTERED_EMAIL_RESPONSE.png
            ├── TC-AUTH-001_VALID_LOGIN_REQUEST.png
            ├── TC-AUTH-001_VALID_LOGIN_RESPONSE.png
            ├── TC-AUTH-002_INVALID_PASSWORD_REQUEST.png
            ├── TC-AUTH-002_INVALID_PASSWORD_RESPONSE.png
            ├── TC-AUTH-003_UNREGISTERED_EMAIL_REQUEST.png
            ├── TC-AUTH-003_UNREGISTERED_EMAIL_RESPONSE.png
            ├── TC-AUTH-004_MISSING_EMAIL_REQUEST.png
            └── TC-AUTH-004_MISSING_EMAIL_RESPONSE.png
```

This is the intended repository tree **after the Authentication milestone is pushed**. Additional folders for automation, test data, and CI/CD will be added as those milestones are implemented.
---

## Environment Notes and Limitations

### Shared Public Environment

ServeRest uses a public testing environment. Test data may be reset or modified independently of this portfolio.

Tests must not assume records created during earlier sessions remain available.

### Test Data Dependencies

Some scenarios depend on data created by earlier requests.

For example:

1. Create a user.
2. Capture the generated user ID.
3. Retrieve the user using that ID.
4. Validate the returned user information.

Future automation will manage these dependencies dynamically rather than rely on hard-coded IDs.

### Error Messages

Some ServeRest API responses use Portuguese error messages. Assertions should use the actual documented or observed response values.

### Current Coverage

The recorded manual testing covers four User Management scenarios and four Authentication scenarios. Products, Cart, API Automation, CI/CD, and broader authorization behavior remain outside the completed scope.

The exact required error HTTP status/message for the Authentication missing-email test (`TC-AUTH-004`) remains unverified against an independent API contract, even though the rejection behavior was observed.

### Sensitive Information

Only disposable test credentials should be used.

Real passwords, authentication tokens, API keys, and other secrets must not be committed to this public repository.

---

## Next Milestones

### Milestone 2 — Authentication Testing (Completed: Manual Behavior Checks)

- Four Authentication scenarios designed, executed, and documented.
- Request/response evidence saved; setup and precondition checks recorded separately.
- Error-response contract clarification remains open for TC-AUTH-004.

### Milestone 3 — Products and Cart Testing

- Test selected product management scenarios.
- Test selected cart workflows.
- Validate authorization and data dependencies where applicable.
- Record test results and evidence.

### Milestone 4 — API Automation

- Add Postman test scripts and assertions.
- Introduce reusable variables.
- Implement request chaining.
- Use dynamic test data.
- Implement selected data-driven scenarios.
- Add response schema checks where appropriate.

### Milestone 5 — CI/CD

- Execute automated tests using Newman.
- Integrate execution into GitHub Actions.
- Generate test reports.
- Publish execution artifacts.
- Document how to reproduce the automated test runs.

### Milestone 6 — Final Portfolio Review

- Review test coverage and traceability.
- Verify documentation and evidence references.
- Review automation reliability.
- Document known limitations and remaining risks.
- Finalize the portfolio for job applications.

---

## References and Attribution

- [ServeRest — Official API Documentation](https://serverest.dev/)
- [ServeRest — Official GitHub Repository](https://github.com/ServeRest/ServeRest)

This repository is an independent QA learning and portfolio project. It is not affiliated with or endorsed by the ServeRest maintainers.
