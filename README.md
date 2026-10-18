# ServeRest API Testing Portfolio

> **Work in Progress** | Current Milestone: **User Management — Manual API Testing Completed**

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

**Current Progress (18 October 2026):** Four User Management manual API test cases have been executed and passed. Other modules, automation, and CI/CD activities are planned.

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
| Authentication | Login and authorization scenarios | Planned |
| Products | Product API scenarios | Planned |
| Cart | Cart API scenarios | Planned |
| API Automation | Postman assertions, variables, request chaining, data-driven testing | Planned |
| CI/CD | Newman and GitHub Actions | Planned |

**Scope Note:** User Management completion refers only to the four documented manual test cases, not complete coverage of all User Management features.

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

Each completed manual test case includes two screenshots:

- **Request Evidence:** Postman request configuration and test data.
- **Response Evidence:** Actual HTTP status and API response.

### TC-USER-001 — Create User

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-001_CREATE_USER_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-001_CREATE_USER_RESPONSE.png)

### TC-USER-002 — Duplicate Email

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-002_DUPLICATE_EMAIL_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-002_DUPLICATE_EMAIL_RESPONSE.png)

### TC-USER-003 — Missing Email

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-003_MISSING_EMAIL_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-003_MISSING_EMAIL_RESPONSE.png)

### TC-USER-004 — Get User by ID

- [View Request Screenshot](evidence/manual-api/user-management/TC-USER-004_GET_USER_REQUEST.png)
- [View Response Screenshot](evidence/manual-api/user-management/TC-USER-004_GET_USER_RESPONSE.png)

All eight evidence files are included in the repository.

The Excel workbook provides the detailed test design and recorded execution results, while the screenshots provide supporting evidence for the manual API executions.

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
        └── user-management/
            ├── TC-USER-001_CREATE_USER_REQUEST.png
            ├── TC-USER-001_CREATE_USER_RESPONSE.png
            ├── TC-USER-002_DUPLICATE_EMAIL_REQUEST.png
            ├── TC-USER-002_DUPLICATE_EMAIL_RESPONSE.png
            ├── TC-USER-003_MISSING_EMAIL_REQUEST.png
            ├── TC-USER-003_MISSING_EMAIL_RESPONSE.png
            ├── TC-USER-004_GET_USER_REQUEST.png
            └── TC-USER-004_GET_USER_RESPONSE.png
```

This structure represents the files currently tracked in Git. Additional folders for automation, test data, and CI/CD will be added as those milestones are implemented.

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

The recorded manual testing covers four User Management scenarios only.

Authentication, Products, Cart, API Automation, and CI/CD are not yet completed.

### Sensitive Information

Only disposable test credentials should be used.

Real passwords, authentication tokens, API keys, and other secrets must not be committed to this public repository.

---

## Next Milestones

### Milestone 2 — Authentication Testing

- Design positive and negative authentication scenarios.
- Execute manual API tests.
- Document expected and actual results.
- Capture execution evidence.

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
