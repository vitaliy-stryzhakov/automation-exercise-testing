# BUG-API-01 — API returns HTTP 200 OK for error responses

**Project:** Automation Exercise  
**Module:** API  
**Severity:** Minor (provisional)  
**Priority:** Medium (provisional)  
**Status:** New  
**Environment:** Windows, Postman  
**Related test cases:** TC-API-02, TC-API-04, TC-API-06, TC-API-08, TC-API-09, TC-API-11, TC-API-12

## Description

When a request is invalid or cannot be processed (unsupported method, missing required parameter, invalid credentials), the API returns HTTP status 200 OK. The actual error code is reported only in the `responseCode` field of the response body.

The behavior was reproduced on four endpoints: `productsList`, `brandsList`, `searchProduct` and `verifyLogin`.

## Preconditions

- The API is available.

## Steps to Reproduce

### Scenario 1 — Unsupported request method

1. Create a `POST` request to `https://automationexercise.com/api/productsList`.
2. Do not add a request body.
3. Send the request.
4. Compare the HTTP status with the `responseCode` in the response body.

### Scenario 2 — Missing required parameter

1. Create a `POST` request to `https://automationexercise.com/api/searchProduct`.
2. Do not add the `search_product` parameter.
3. Send the request.
4. Compare the HTTP status with the `responseCode` in the response body.

### Scenario 3 — Invalid credentials

1. Create a `POST` request to `https://automationexercise.com/api/verifyLogin`.
2. In the form-data body, add `email` = `qa.nonexistent.user@example.com` and `password` = `WrongPass123`.
3. Send the request.
4. Compare the HTTP status with the `responseCode` in the response body.

## Expected Result

The HTTP status matches the error reported in the response body:

- Scenario 1: 405 Method Not Allowed.
- Scenario 2: 400 Bad Request.
- Scenario 3: 404 Not Found.

The response body contains the `responseCode` and `message` described in the API List.

## Actual Result

In all scenarios, the HTTP status is 200 OK. The response bodies match the API List:

| Scenario | HTTP status | `responseCode` | `message` |
|---|---|---:|---|
| 1 | 200 OK | 405 | This request method is not supported. |
| 2 | 200 OK | 400 | Bad request, search_product parameter is missing in POST request. |
| 3 | 200 OK | 404 | User not found! |

## Additional Evidence

The same behavior was observed in all error test cases:

| Test case | Request | HTTP status | `responseCode` |
|---|---|---:|---:|
| TC-API-02 | `POST /productsList` | 200 | 405 |
| TC-API-04 | `PUT /brandsList` | 200 | 405 |
| TC-API-06 | `POST /searchProduct` without parameter | 200 | 400 |
| TC-API-08 | `POST /verifyLogin`, non-existent user | 200 | 404 |
| TC-API-09 | `POST /verifyLogin` without `email` | 200 | 400 |
| TC-API-11 | `POST /verifyLogin`, incorrect password | 200 | 404 |
| TC-API-12 | `DELETE /verifyLogin` | 200 | 405 |

For successful requests (TC-API-01, 03, 05, 07, 10), the HTTP status and the `responseCode` are both 200, so the mismatch occurs only in error responses.

## Severity and Priority Notes

Severity and priority are provisional because the API List describes only the `responseCode` and `message` in the response body and does not explicitly require a matching HTTP status.

The issue does not affect users of the website. However, it is systemic: HTTP clients, monitoring tools and automated checks that rely on the HTTP status treat failed requests as successful, and clients must parse the response body to detect errors. This is why the priority is higher than in a single-endpoint issue.