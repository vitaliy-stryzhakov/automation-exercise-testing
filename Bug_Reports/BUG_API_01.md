# BUG-API-01 — Unsupported request method returns HTTP 200 instead of 405

**Project:** Automation Exercise  
**Module:** API  
**Severity:** Minor (provisional)  
**Priority:** Low (provisional)  
**Status:** New  
**Environment:** Windows, Postman  
**Related test case:** TC-API-02

## Description

When an unsupported request method is sent to an API endpoint, the server returns HTTP status 200 OK. The error is reported only inside the response body (`responseCode` 405).

## Preconditions

- The API is available.

## Steps to Reproduce

1. Create a `POST` request to `https://automationexercise.com/api/productsList`.
2. Do not add a request body.
3. Send the request.
4. Compare the HTTP status with the `responseCode` in the response body.

## Expected Result

The HTTP status is 405 Method Not Allowed. The response body contains `responseCode` 405 and the message `This request method is not supported.`

## Actual Result

The HTTP status is 200 OK. The response body contains the expected error:

```json
{"responseCode": 405, "message": "This request method is not supported."}
```

## Additional Evidence

- The `Content-Type` header is `text/html; charset=utf-8`, although the body is JSON.
- The `allow` header lists `POST, GET, DELETE, OPTIONS, PUT`, which does not match the actual behavior of the endpoint.
- Only the `productsList` endpoint was checked. Other endpoints may behave the same way.

## Severity and Priority Notes

Severity and priority are provisional because the API documentation describes only the `responseCode` in the body and does not explicitly require the HTTP status.

The issue does not affect users of the website, but it may mislead API clients and automated checks that rely on the HTTP status.