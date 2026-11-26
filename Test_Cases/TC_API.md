# API Module — Test Cases

**Project:** Automation Exercise  
**Module:** API  
**Test type:** Manual API Testing  
**Test environment:** Windows, Postman  
**Test status:** In progress

**Base URL:** `https://automationexercise.com/api`  
**Source of requirements:** [API List](https://automationexercise.com/api_list)

**Evaluation approach:** The API List describes only the `responseCode` and `message` in the response body. For error cases, the expected HTTP status is the same as the `responseCode` documented in the API List, which is the standard way to report errors over HTTP. A test case is marked FAIL if the HTTP status differs from the expected one, even when the response body matches the API List.

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

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not. See the evaluation approach above. The `allow` header is described in API-OBS-03.

---

### TC-API-03 — Get all brands list

**Preconditions:**
- The API is available.

**Request:**
- Method: `GET`
- URL: `https://automationexercise.com/api/brandsList`
- Body: none

**Expected Result:**
- The HTTP status is 200 OK.
- The response body contains `responseCode` 200 and a list of all brands.

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 200.
- The `brands` array contains 34 entries, each with `id` and `brand`.
- The array contains 8 unique brand names: Polo, H&M, Madame, Mast & Harbour, Babyhug, Allen Solly Junior, Kookie Kids, Biba.
- The brand names match the brands shown in the UI sidebar.

**Status:** PASS

**Note:** The list contains one entry per product, not per brand, so brand names are duplicated. The `id` values match the product ids from `productsList`. See API-OBS-04. The `Content-Type` header is `text/html; charset=utf-8`. See API-OBS-01.

---

### TC-API-04 — Send an unsupported request method (PUT) to the brands list endpoint

**Preconditions:**
- The API is available.

**Request:**
- Method: `PUT`
- URL: `https://automationexercise.com/api/brandsList`
- Body: none

**Expected Result:**
- The HTTP status is 405 Method Not Allowed.
- The response body contains `responseCode` 405 and the message `This request method is not supported.`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 405.
- `message`: `This request method is not supported.`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not.

---

### TC-API-05 — Search for an existing product

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/searchProduct`
- Body (form-data):
  - `search_product`: `top`

**Expected Result:**
- The HTTP status is 200 OK.
- The response body contains `responseCode` 200 and a list of the searched products.

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 200.
- The `products` array contains 14 products with the same structure as in `productsList`.
- The number of products matches the UI search for `top` (see TC-PRODUCTS-10).
- Two of the returned products (ids 18 and 24) do not contain `top` in their names. They belong to the category `Tops & Shirts`.

**Status:** PASS

**Note:** The search matches both the product name and the category. See API-OBS-05.

---

### TC-API-06 — Search without the required parameter

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/searchProduct`
- Body: none (the `search_product` parameter is not sent)

**Expected Result:**
- The HTTP status is 400 Bad Request.
- The response body contains `responseCode` 400 and the message `Bad request, search_product parameter is missing in POST request.`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 400.
- `message`: `Bad request, search_product parameter is missing in POST request.`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not.

---

### TC-API-07 — Search for a non-existent product

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/searchProduct`
- Body (form-data):
  - `search_product`: `qwertyxyz`

**Expected Result:**
- The HTTP status is 200 OK.
- The response body contains `responseCode` 200 and an empty `products` list.

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 200.
- The `products` array is empty (`[]`).
- The result matches the UI behavior (see TC-PRODUCTS-07).

**Status:** PASS

---

### TC-API-08 — Verify login with a non-existent user

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/verifyLogin`
- Body (form-data):
  - `email`: `qa.nonexistent.user@example.com`
  - `password`: `WrongPass123`

**Expected Result:**
- The HTTP status is 404 Not Found.
- The response body contains `responseCode` 404 and the message `User not found!`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 404.
- `message`: `User not found!`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not.

---

### TC-API-09 — Verify login with a missing email parameter

**Preconditions:**
- The API is available.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/verifyLogin`
- Body (form-data):
  - `password`: `WrongPass123`
  - The `email` parameter is not sent.

**Expected Result:**
- The HTTP status is 400 Bad Request.
- The response body contains `responseCode` 400 and the message `Bad request, email or password parameter is missing in POST request.`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 400.
- `message`: `Bad request, email or password parameter is missing in POST request.`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not. The message does not say which parameter is missing. See API-OBS-07.

---

### TC-API-10 — Verify login with valid credentials

**Preconditions:**
- The API is available.
- A registered user account exists.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/verifyLogin`
- Body (form-data):
  - `email`: Registered test account email (redacted)
  - `password`: Valid password (redacted)

**Expected Result:**
- The HTTP status is 200 OK.
- The response body contains `responseCode` 200 and the message `User exists!`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 200.
- `message`: `User exists!`

**Status:** PASS

---

### TC-API-11 — Verify login with a registered email and an incorrect password

**Preconditions:**
- The API is available.
- A registered user account exists.

**Request:**
- Method: `POST`
- URL: `https://automationexercise.com/api/verifyLogin`
- Body (form-data):
  - `email`: Registered test account email (redacted)
  - `password`: `WrongPass123` (incorrect password)

**Expected Result:**
- The HTTP status is 404 Not Found.
- The response body contains `responseCode` 404 and the message `User not found!`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 404.
- `message`: `User not found!`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not. The message is the same as for a non-existent user (TC-API-08), although the user exists. See API-OBS-06.

---

### TC-API-12 — Send an unsupported request method (DELETE) to the verify login endpoint

**Preconditions:**
- The API is available.

**Request:**
- Method: `DELETE`
- URL: `https://automationexercise.com/api/verifyLogin`
- Body: none

**Expected Result:**
- The HTTP status is 405 Method Not Allowed.
- The response body contains `responseCode` 405 and the message `This request method is not supported.`

**Actual Result:**
- HTTP status: 200 OK.
- `responseCode` in the body: 405.
- `message`: `This request method is not supported.`

**Status:** FAIL

**Related bug:** BUG-API-01

**Note:** The response body matches the API List. The HTTP status does not.

---

## API Observations

These observations were identified during API testing. They are not confirmed defects because formal API requirements were not available.

### API-OBS-01 — Content-Type header does not match the response body

**Observation:**
The responses of `GET /productsList`, `POST /productsList` and `GET /brandsList` have the header `Content-Type: text/html; charset=utf-8`, although the body is JSON. Headers of the other requests were not recorded.

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
The `allow` header lists `POST`, `PUT` and `DELETE` for `/productsList` and `/brandsList`, while the API List describes only `GET` for both endpoints. The order of methods differs between responses.

**Impact:**
The header may mislead API clients about which methods are available.

**Suggestion:**
Return only the methods that the endpoint actually supports.

---

### API-OBS-04 — Brands list contains duplicates and uses product ids

**Observation:**
`GET /brandsList` returns 34 entries for 8 unique brands. Brand names are repeated (for example, Madame and Polo), and the `id` values are the same as the product ids from `productsList`, including the gaps in numbering.

**Impact:**
Clients that expect a list of unique brands must remove duplicates themselves. The `id` cannot be used as a brand identifier.

**Suggestion:**
Return each brand once with its own unique id, or rename the endpoint to reflect that it returns product-brand pairs.

---

### API-OBS-05 — Product search matches both the name and the category

**Observation:**
`POST /searchProduct` with `search_product` = `top` returned 14 products. Two of them (Little Girls Mr. Panda Shirt and Colour Blocked Shirt – Sky Blue) do not contain `top` in their names and were found by the category `Tops & Shirts`. The UI search returns the same 14 products.

**Impact:**
Users and API clients may not expect results that do not match the product name.

**Suggestion:**
Describe the search rules in the API documentation, or limit the search to product names.

---

### API-OBS-06 — The message "User not found!" is returned for an existing user with an incorrect password

**Observation:**
`POST /verifyLogin` returns `User not found!` both for a non-existent email (TC-API-08) and for an existing email with an incorrect password (TC-API-11).

**Impact:**
The message is inaccurate when the user exists. In the UI, the message `Your email or password is incorrect!` describes both cases correctly.

**Suggestion:**
Use a message that covers both cases, for example, `Invalid email or password`.

---

### API-OBS-07 — The missing-parameter message does not name the missing parameter

**Observation:**
The message `Bad request, email or password parameter is missing in POST request.` mentions both parameters. It was received when only `email` was missing.

**Impact:**
The client cannot tell from the message which parameter must be added.

**Suggestion:**
Name the specific missing parameter in the message.

---

## Test Execution Summary

| Result | Count |
|---|---:|
| PASS | 5 |
| FAIL | 7 |
| Total | 12 |

**Coverage:**
- Tested: `productsList`, `brandsList`, `searchProduct`, `verifyLogin`.
- Not tested yet: `createAccount`, `getUserDetailByEmail`, `updateAccount`, `deleteAccount`.

**Additional findings:**
- 1 confirmed issue (the API returns HTTP 200 for error responses), documented in a separate bug report: BUG-API-01. All 7 failed test cases are caused by this issue.
- 7 API observations recorded for further review.

**Conclusion:** _To be filled after all planned endpoints are tested._