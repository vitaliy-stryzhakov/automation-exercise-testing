# Automation Exercise — Manual QA Project

Practice project in manual software testing of the [Automation Exercise](https://automationexercise.com/) e-commerce website. It includes a test plan, test cases, bug reports and a summary of the results.

## Scope

- Login and Logout
- Shopping Cart
- Products (list, details, search, categories and brands, reviews)
- API (manual testing with Postman) — _planned_

## Repository Structure

| File | Description |
|---|---|
| [Test_Plan.md](Test_Plan/Test_Plan.md) | Objectives, scope, approach, environment, deliverables |
| [TC_LOGIN.md](Test_Cases/TC_LOGIN.md) | 8 test cases for Login and Logout |
| [TC_CART.md](Test_Cases/TC_CART.md) | 16 test cases and 2 UI observations for Cart |
| [TC_PRODUCTS.md](Test_Cases/TC_PRODUCTS.md) | 18 test cases and 4 UI observations for Products |
| [BUG_LOGIN_01.md](Bug_Reports/BUG_LOGIN_01.md) | Password visibility icon disappears after losing focus |
| [BUG_CART_01.md](Bug_Reports/BUG_CART_01.md) | Application accepts zero and negative product quantities |
| Test Summary Report | _planned_ |

## Results at a Glance

| Module | Test cases | PASS | FAIL |
|---|---:|---:|---:|
| Login and Logout | 8 | 7 | 1 |
| Cart | 16 | 12 | 4 |
| Products | 18 | 18 | 0 |
| **Total** | **42** | **37** | **5** |

**Defects found:** 2

- **BUG-CART-01** (Major, provisional): zero and negative quantities are accepted, reach the checkout and open the payment form.
- **BUG-LOGIN-01** (Minor, provisional): the password visibility icon disappears after the field loses focus.

## Approach

- **Type:** manual testing
- **Techniques:** functional, positive, negative, UI testing
- **Environment:** Windows, Microsoft Edge
- **Documentation style:** a unified format for all test cases and bug reports (preconditions, steps, expected and actual results, status), with cross-references between test cases and bugs

## Limitations

- Only one browser was used.
- Severity and priority are provisional because no formal requirements were available.
- No payment was submitted during testing.
- Automated, performance and security testing are out of scope.

## Author

[Vitaliy Stryzhakov](https://www.linkedin.com/in/vitaliy-stryzhakov-031a57275)