# API Module — Test Cases

**Project:** Automation Exercise  
**Module:** API  
**Test type:** Manual API Testing  
**Test environment:** Windows, Postman  
**Test status:** In progress

**Base URL:** `https://automationexercise.com/api`  
**Source of requirements:** [API List](https://automationexercise.com/api_list)

## Test Cases

### TC-API-01 — Get all products list

**Preconditions:**
- The API is available.

**Request:**
- Method: `GET`
- URL: `https://automationexercise.com/api/productsList`
- Body: none

**Expected Result:**
- The HTTP status is 200 OK.
- The response body contains `responseCode` 200 and a list of all products.

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 200.
- The `products` array contains 34 products.
- Each product has `id`, `name`, `price`, `brand` and `category` (with `usertype` and `category`).
- Blue Top: price `Rs. 500`, brand `Polo`, category Women / Tops. The price matches the UI (see TC-CART-03).

**Status:** PASS

**Note:** The `Content-Type` header is `text/html; charset=utf-8`, although the body is JSON. See API-OBS-01. The price is returned as a string (`Rs. 500`). See API-OBS-02.

---

### TC-API-02 — Send an unsupported request method (POST) to the products list endpoint

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/productsList`
- Body: none

**Expected Result:**
- The HTTP status is 405 Method Not Allowed.
- The response body contains `responseCode` 405 and the message `This request method is not supported.`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 405.
- `message`: `This request method is not supported.`
- The `allow` header lists `POST, GET, DELETE, OPTIONS, PUT`.

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The API List describes only the `responseCode` in the body and does not mention the HTTP status. The expected HTTP status 405 is based on the HTTP standard.

---

## API Observations

These observations were identified during API testing. They are not confirmed defects because formal API requirements were not available.

### API-OBS-01 — Content-Type header does not match the response body

**Observation:**
The responses of `GET /productsList` and `POST /productsList` have the header `Content-Type: text/html; charset=utf-8`, although the body is JSON.

**Impact:**
API clients may process the response incorrectly because they rely on `Content-Type` to choose a parser.

**Suggestion:**
Return `Content-Type: application/json`. Check the remaining endpoints to confirm whether this is system-wide.

---

### API-OBS-02 — Price is returned as a string with a currency prefix

**Observation:**
The `price` field is returned as a string (for example, `"Rs. 500"`) instead of a number.

**Impact:**
Clients must parse the string before using the price in calculations.

**Suggestion:**
Consider returning the price as a number and the currency as a separate field.

---

### API-OBS-03 — The allow header does not reflect the supported methods

**Observation:**
The `allow` header lists `POST`, `PUT` and `DELETE` for `/productsList`, while the endpoint supports only `GET`. The order of methods differs between responses.

**Impact:**
The header may mislead API clients about which methods are available.

**Suggestion:**
Return only the methods that the endpoint actually supports.

---

## Test Execution Summary

| Result | Count |
|---|---:|
| PASS | 1 |
| FAIL | 1 |
| Total | 2 |

**Additional findings:**
- 1 confirmed issue (HTTP status differs from `responseCode`), documented in a separate bug report: BUG-API-01.
- 3 API observations recorded for further review.

**Conclusion:** _To be filled after all planned endpoints are tested._