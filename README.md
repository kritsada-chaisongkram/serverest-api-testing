# ServeRest API Testing Portfolio

**Manual API Testing: 16 test cases | API Automation: 8 test scenarios | Test Data Cleanup**

## Project Overview

I used Postman to practice API testing with [ServeRest](https://serverest.dev/), a public e-commerce API. I wrote test cases, sent API requests, checked the responses, and saved screenshots of the results.

My tests cover User Management, Authentication, Products, and Cart. I automated selected scenarios using Postman scripts and Newman. I later added cleanup requests to remove test data created during automation.

## Quick Portfolio Review

| Item | Details |
|---|---|
| Tools | Postman, JavaScript, Newman, Git/GitHub, GitHub Actions |
| Manual testing | 16 test cases across 4 modules |
| Recorded manual results | 16 PASS* |
| API automation | 8 test scenarios, plus setup requests |
| Newman result (with cleanup) | 27 requests, 47 assertions passed, 0 failures |
| Reliability test | 3 iterations, 141 assertions passed, 0 failures |
| GitHub Actions | CI workflow passed before cleanup; updated collection pending CI verification |
| Data-driven login | 3 iterations, 6 assertions passed |
| Test documentation | [Test Cases and Execution Results](test-documentation/ServeRest_API_Test_Cases.xlsx) |
| Manual screenshots | [View Manual Evidence](evidence/manual-api/) |
| Automation screenshots | [View Automation Evidence](evidence/automation/) |

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

## How I Tested Manually

1. Choose a scenario and write the expected result.
2. Prepare the user, product, or cart data needed for the test.
3. Send the request in Postman.
4. Check the HTTP status, response body, and related data when needed.
5. Record the actual result and save screenshots.

The Excel workbook has two sheets: **Test Cases** (steps and expected results) and **Test Execution** (actual results, status, and evidence links).

### Manual Test Evidence

- [User Management](evidence/manual-api/user-management/)
- [Authentication](evidence/manual-api/authentication/)
- [Products](evidence/manual-api/products/)
- [Cart](evidence/manual-api/cart/)

Some tests also have setup or verification screenshots. For example, Cart tests include checks of stock or cart data.

## API Automation

I automated these 8 test cases using JavaScript assertions in Postman:

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

I used setup requests and Postman variables to create users and products, reuse IDs and authorization tokens, and avoid fixed test data where possible. The collection now includes cleanup and verification requests.

### Automated Test Results

| Run | Result |
|---|---|
| Postman Collection Runner — API Automation with cleanup | 27 requests, 47 assertions passed, 0 failures (1 iteration) |
| Reliability test — API Automation with cleanup | 3 iterations, 141 assertions passed, 0 failures |
| Newman CLI — API Automation with cleanup | 27 requests, 47 assertions passed, 0 failures |
| Postman Data-Driven Login | 3 iterations, 6 assertions passed, 0 failures |

These are results from recorded runs, not a guarantee that future runs will always pass. The original automation run (before cleanup) had 13 requests and 33 assertions.

### Test Data Cleanup

The `API Automation` folder runs the automated scenarios first, followed by 7 cleanup requests and 7 verification requests. Cleanup covers the cart, products, and users created during the run.

- Store the IDs of newly created test data in Postman variables.
- Clear old IDs before creating new test data to avoid using values from previous runs.
- Cancel the test cart using its owner's authorization token, then delete the test products and users.
- Send GET requests after cleanup to check that the resources no longer exist.

In my recorded runs, the cleanup requests and verification checks passed. The tests use the shared ServeRest public API, so results can change if the service or its data changes.

### Run API Automation with Newman

Install Node.js and Newman, then run the following commands from the project root in PowerShell:

```powershell
npm.cmd install -g newman
newman.cmd run ".\postman\serverest.postman_collection.json" --environment ".\postman\serverest.postman_environment.json" --folder "API Automation"
```

To export a detailed JSON report locally:

```powershell
New-Item -ItemType Directory -Path ".\reports" -Force
newman.cmd run ".\postman\serverest.postman_collection.json" --environment ".\postman\serverest.postman_environment.json" --folder "API Automation" --reporters cli,json --reporter-json-export ".\reports\newman-report.json"
```

The `reports/` folder is ignored by Git because raw Newman JSON reports can contain tokens and other request or response data.

### Data-Driven Login Testing

I used [login-test-data.csv](test-data/login-test-data.csv) to test three invalid passwords. Each test expects HTTP 401. The Postman Runner result shows 3 iterations and 6 passed assertions (including setup requests).

This is a separate run from the `API Automation` folder. The CSV is used with the `Data-Driven Testing` folder in Postman Runner.

### Automation Evidence

- **Postman scripts:** [Create User](evidence/automation/postman/user-create-pass.png), [Duplicate Email](evidence/automation/postman/duplicate-email-test.png), [Create Product](evidence/automation/postman/product-create-pass.png), [Create Cart](evidence/automation/postman/cart-create-pass.png)
- **Variables and runner:** [Dynamic Setup](evidence/automation/postman/request-chaining-setup.png), [Valid Login Runner](evidence/automation/postman/valid-login-runner.png)
- **Full run:** [Collection Runner — 33 passed](evidence/automation/collection-runner/automation-collection-run-pass.png)
- **Data-driven:** [Login Data-Driven Runner — 6 passed](evidence/automation/data-driven/login-data-driven-pass.png)
- **Newman (original run):** [Execution — Part 1](evidence/automation/newman/newman-cli-execution%201.png), [Execution — Part 2](evidence/automation/newman/newman-cli-execution%202.png), [Summary — 33 assertions passed](evidence/automation/newman/newman-cli-summary.png)
- **Newman with cleanup:** [Summary — 47 assertions passed](evidence/automation/newman/newman-cleanup-summary.png)
- **Cleanup and reliability:** [Postman Runner — 3 iterations, 141 passed](evidence/automation/cleanup/cleanup-test-pass.png)
- **GitHub Actions:** [Successful CI workflow (before cleanup)](evidence/automation/github-actions/ci-workflow-pass.png)

## GitHub Actions CI

GitHub Actions runs the `API Automation` folder with Newman after pushes to `main` and pull requests targeting `main`. The workflow uploads a JUnit test report as an artifact.

The workflow passed when first set up and after upgrading the GitHub Actions versions. Those runs used the **earlier collection without cleanup**. The updated 27-request collection passed locally with Newman; its GitHub Actions run still needs verification after the latest collection is pushed.

Workflow: [ServeRest API Tests](.github/workflows/api-tests.yml) | [GitHub Actions runs](https://github.com/kritsada-chaisongkram/serverest-api-testing/actions)

## Notes

- The tests use the shared public ServeRest API (`https://serverest.dev`). Test data can change or reset.
- Some API messages are in Portuguese. I recorded the messages returned by the API.
- The 16 manual PASS results describe the recorded test runs, not full API coverage.
- TC-AUTH-004 still needs confirmation of the exact expected error response.
- Only test accounts should be used. Passwords, active tokens, and API keys should not be shared in the repository.
- The cleanup results have been verified in Postman Runner and local Newman. Updated GitHub Actions CI results are pending.

## Next Steps

1. Commit and push the updated collection, README, and screenshots.
2. Confirm that GitHub Actions passes with 27 requests and 47 assertions.
3. Check the repository files and evidence links before completing the portfolio.

## References

- [ServeRest API Documentation](https://serverest.dev/)
- [ServeRest GitHub](https://github.com/ServeRest/ServeRest)

This is my independent practice project, not an official ServeRest test suite.
