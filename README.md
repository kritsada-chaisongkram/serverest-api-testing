# ServeRest API Testing Portfolio

**Manual API Testing: 16 test cases completed** | **API Automation: Planned**

## Project Overview

This is a QA portfolio project using the [ServeRest](https://serverest.dev/) practice e-commerce REST API. I used Postman to design and execute positive and negative API tests, review responses, and record test results with screenshots.

The project covers four API modules. A separate automation phase using Postman scripts, Newman, and GitHub Actions is planned.

## Quick Portfolio Review

| Item | Details |
|---|---|
| Project | ServeRest API Testing |
| Testing Type | Manual REST API Testing (Postman) |
| Modules Tested | User Management, Authentication, Products, Cart |
| Manual Test Results | 16 recorded PASS results across 16 test cases* |
| Test Documentation | [Test Cases & Execution Results](test-documentation/ServeRest_API_Test_Cases.xlsx) |
| Test Evidence | [View Screenshots](evidence/manual-api/) |
| API Automation | Planned — 8 selected scenarios |

*One Authentication negative case passed the observed rejection behavior, but its exact error-response contract still needs independent confirmation. Results do not imply complete API coverage.*

## Tools and Environment

| Item | Details |
|---|---|
| API | [ServeRest](https://serverest.dev/) |
| Base URL | `https://serverest.dev` |
| Testing tool | Postman |
| Test documentation | Excel |
| Version control | Git and GitHub |
| Test environment | Shared public API |

## Manual Testing Summary

| Module | Test Cases | Passed |
|---|---:|---:|
| User Management | 4 | 4 |
| Authentication | 4 | 4* |
| Products | 4 | 4 |
| Cart | 4 | 4 |
| **Total** | **16** | **16*** |

*The Authentication missing-email case passed the observed rejection behavior; its exact error-response contract still needs independent confirmation. Results describe the recorded manual executions, not complete API coverage.*

### Test Scenarios

| Test Case ID | Scenario | Recorded Result |
|---|---|---|
| TC-USER-001 | Create valid user | PASS |
| TC-USER-002 | Reject duplicate email | PASS |
| TC-USER-003 | Reject missing email | PASS |
| TC-USER-004 | Get user by ID | PASS |
| TC-AUTH-001 | Valid login | PASS |
| TC-AUTH-002 | Reject invalid password | PASS |
| TC-AUTH-003 | Reject unregistered email | PASS |
| TC-AUTH-004 | Reject missing email | PASS* |
| TC-PROD-001 | Get product list | PASS |
| TC-PROD-002 | Get product by ID | PASS |
| TC-PROD-003 | Create valid product | PASS |
| TC-PROD-004 | Reject duplicate product name | PASS |
| TC-CART-001 | Create cart with valid product | PASS |
| TC-CART-002 | Reject second cart for same user | PASS |
| TC-CART-003 | Reject cart with insufficient stock | PASS |
| TC-CART-004 | Reject cart with nonexistent product | PASS |

## Testing Approach

1. Review API behavior and identify positive and negative scenarios.
2. Prepare test data and check prerequisites (such as user login, existing products, or available stock).
3. Send requests using Postman.
4. Compare HTTP status codes and response data with expected results.
5. Perform supporting GET checks when needed, such as confirming stock or cart details.
6. Record actual results and capture request/response evidence.

Test cases and execution results are recorded in a two-sheet Excel workbook:

- **Test Cases:** Preconditions, request data, test steps, and expected results.
- **Test Execution:** Actual results, PASS/FAIL, evidence paths, and remarks.

**[View Manual Test Cases and Execution Results](test-documentation/ServeRest_API_Test_Cases.xlsx)**

## Test Evidence

Screenshots are organized by module. Each case has request/response evidence, with additional setup or verification screenshots where needed.

- [User Management evidence](evidence/manual-api/user-management/)
- [Authentication evidence](evidence/manual-api/authentication/)
- [Products evidence](evidence/manual-api/products/)
- [Cart evidence](evidence/manual-api/cart/)

Evidence screenshots should not include passwords, active Bearer tokens, or API keys. File paths in the workbook should be checked against the committed screenshots.

## Automation — Planned

Eight manual scenarios have been selected as the starting scope for automation:

| Test Case ID | Planned Automation Scenario |
|---|---|
| TC-USER-001 | Create valid user |
| TC-USER-002 | Reject duplicate email |
| TC-AUTH-001 | Valid login |
| TC-AUTH-002 | Reject invalid password |
| TC-PROD-003 | Create valid product |
| TC-PROD-004 | Reject duplicate product name |
| TC-CART-001 | Create valid cart |
| TC-CART-003 | Reject insufficient stock |

Planned work includes JavaScript assertions, variables, request chaining, fresh test data, Newman reports, and GitHub Actions. **These automated tests and CI runs are not yet complete.**

## Project Structure

```text
serverest-api-testing/
├── README.md
├── test-documentation/
│   └── ServeRest_API_Test_Cases.xlsx
├── evidence/
│   └── manual-api/
│       ├── user-management/
│       ├── authentication/
│       ├── products/
│       └── cart/
└── postman/                 # Collection/automation work to be added
```

## Notes and Limitations

- ServeRest is a shared public API. Test records and product stock may change or reset, so prerequisites must be checked before each run.
- Some responses use Portuguese messages; recorded actual results keep the API's original wording.
- TC-AUTH-004: the missing-email request was rejected, but the exact expected error status/message contract has not been independently confirmed.
- A rejected request and a follow-up lookup are documented separately when used as supporting evidence; results are not claimed beyond what was checked.
- Use only disposable test accounts. Do not commit passwords, Bearer tokens, or Vault keys.

## Next Steps

**Completed:** Manual API testing (16 test cases), execution documentation, evidence links, and GitHub publication.

1. Automate the eight selected scenarios in Postman using JavaScript assertions and reusable setup/test data.
2. Run the collection with Newman and integrate it with GitHub Actions.
3. Document how to reproduce the automated test runs, review results, and finalize the portfolio.

## References

- [ServeRest API Documentation](https://serverest.dev/)
- [ServeRest Official GitHub Repository](https://github.com/ServeRest/ServeRest)

This is an independent QA learning portfolio and is not an official ServeRest test suite.
