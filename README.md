# ServeRest API Testing Portfolio

**Manual API Testing: 16 test cases completed | API Automation: In progress**

## Project Overview

I used Postman to practice API testing with [ServeRest](https://serverest.dev/), a public e-commerce API. I wrote test cases, sent API requests, checked the responses, and saved screenshots of the results.

My manual tests cover User Management, Authentication, Products, and Cart. I am now working on automating selected test cases.

## Quick Portfolio Review

| Item | Details |
|---|---|
| Tool | Postman |
| Manual testing | 16 test cases across 4 modules |
| Recorded results | 16 PASS* |
| Test documentation | [Test Cases and Execution Results](test-documentation/ServeRest_API_Test_Cases.xlsx) |
| Screenshots | [View Test Evidence](evidence/manual-api/) |
| Automation | 8 test cases selected; work in progress |

*TC-AUTH-004 passed the observed missing-email rejection. I have not independently confirmed the exact expected error status and message.*

## Manual Test Results

| Module | Test Cases | Passed |
|---|---:|---:|
| User Management | 4 | 4 |
| Authentication | 4 | 4* |
| Products | 4 | 4 |
| Cart | 4 | 4 |
| **Total** | **16** | **16*** |

### Test Cases

| Test Case ID | Scenario | Result |
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

## How I Tested

1. Choose a scenario and write the expected result.
2. Prepare the user, product, or cart data needed for the test.
3. Send the request in Postman.
4. Check the HTTP status, response body, and related data when needed.
5. Record the actual result and save screenshots.

The Excel workbook has two sheets: **Test Cases** (steps and expected results) and **Test Execution** (actual results, status, and evidence links).

## Test Evidence

Screenshots are saved by module:

- [User Management](evidence/manual-api/user-management/)
- [Authentication](evidence/manual-api/authentication/)
- [Products](evidence/manual-api/products/)
- [Cart](evidence/manual-api/cart/)

Some tests also have setup or verification screenshots. For example, Cart tests include checks of stock or cart data.

## API Automation — In Progress

I selected these 8 cases to automate in Postman:

| Test Case ID | Scenario |
|---|---|
| TC-USER-001 | Create valid user |
| TC-USER-002 | Reject duplicate email |
| TC-AUTH-001 | Valid login |
| TC-AUTH-002 | Reject invalid password |
| TC-PROD-003 | Create valid product |
| TC-PROD-004 | Reject duplicate product name |
| TC-CART-001 | Create valid cart |
| TC-CART-003 | Reject insufficient stock |

I am working on JavaScript assertions, variables, and reusable test data. Newman and GitHub Actions are planned. **Automated test execution and CI reports have not been published yet.**

## Notes

- The tests use the shared public ServeRest API (`https://serverest.dev`). Test data can change or reset.
- Some API messages are in Portuguese. I recorded the messages returned by the API.
- The 16 PASS results describe these manual test runs, not full API coverage.
- TC-AUTH-004 needs confirmation of the exact expected error response.
- Only test accounts should be used. Passwords, active tokens, and API keys should not be shared in the repository.

## Next Steps

1. Finish the 8 selected Postman automated tests with data that can be used again.
2. Run the collection with Newman and GitHub Actions.
3. Add instructions for running the tests, reports, and final portfolio review.

## References

- [ServeRest API Documentation](https://serverest.dev/)
- [ServeRest GitHub](https://github.com/ServeRest/ServeRest)

This is my independent practice project, not an official ServeRest test suite.
