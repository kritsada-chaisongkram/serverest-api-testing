# ServeRest API Testing Portfolio

**Manual API Testing: 16 test cases | Postman API Automation: 8 test scenarios completed**

## Project Overview

I used Postman to practice API testing with [ServeRest](https://serverest.dev/), a public e-commerce API. I wrote test cases, sent API requests, checked the responses, and saved screenshots of the results.

My tests cover User Management, Authentication, Products, and Cart. I also automated selected scenarios using Postman scripts and ran them with Newman.

## Quick Portfolio Review

| Item | Details |
|---|---|
| Tools | Postman, JavaScript, Newman, Git/GitHub |
| Manual testing | 16 test cases across 4 modules |
| Recorded manual results | 16 PASS* |
| API automation | 8 test scenarios, plus setup requests |
| Newman result | 13 requests, 33 assertions passed, 0 failures |
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

I used setup requests and Postman variables to create users and products, reuse IDs and authorization tokens, and avoid fixed test data where possible.

### Automated Test Results

| Run | Result |
|---|---|
| Postman Collection Runner — API Automation | 33 passed, 0 failed |
| Newman CLI — API Automation | 13 requests, 33 assertions passed, 0 failures |
| Postman Data-Driven Login | 3 iterations, 6 assertions passed, 0 failures |

These are results from the recorded runs, not a guarantee that future runs will always pass.

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
- **Newman:** [Execution — Part 1](evidence/automation/newman/newman-cli-execution%201.png), [Execution — Part 2](evidence/automation/newman/newman-cli-execution%202.png), [Summary — 33 assertions passed](evidence/automation/newman/newman-cli-summary.png)

## Notes

- The tests use the shared public ServeRest API (`https://serverest.dev`). Test data can change or reset.
- Some API messages are in Portuguese. I recorded the messages returned by the API.
- The 16 manual PASS results describe the recorded test runs, not full API coverage.
- TC-AUTH-004 still needs confirmation of the exact expected error response.
- Only test accounts should be used. Passwords, active tokens, and API keys should not be shared in the repository.
- GitHub Actions CI is planned for the next phase; CI execution is not yet included in these results.

## Next Steps

1. Add GitHub Actions to run the Newman API Automation folder.
2. Review the CI results and artifacts.
3. Do a final review of the README, test files, and evidence links.

## References

- [ServeRest API Documentation](https://serverest.dev/)
- [ServeRest GitHub](https://github.com/ServeRest/ServeRest)

This is my independent practice project, not an official ServeRest test suite.
