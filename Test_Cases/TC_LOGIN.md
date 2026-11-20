# Login Module — Test Cases

**Project:** Automation Exercise  
**Module:** Login and Logout  
**Test type:** Manual Functional Testing  
**Test environment:** Windows, Microsoft Edge  
**Test status:** Completed

## Test Cases

### TC-LOGIN-01 — Login with empty email and password

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: Empty
- Password: Empty

**Steps:**
1. Leave the Email Address field empty.
2. Leave the Password field empty.
3. Click the Login button.

**Expected Result:**
- The user is not logged in.
- A validation message indicates that the Email Address field is required.
- The user remains on the Login page.

**Actual Result:**
- The user was not logged in.
- A validation message appeared next to the Email Address field, requesting that it be filled in.
- The user remained on the Login page.

**Status:** PASS

---

### TC-LOGIN-02 — Login with valid email and empty password

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: `test@example.com`
- Password: Empty

**Steps:**
1. Enter the email address in the Email Address field.
2. Leave the Password field empty.
3. Click the Login button.

**Expected Result:**
- The user is not logged in.
- A validation message indicates that the Password field is required.
- The user remains on the Login page.

**Actual Result:**
- The user was not logged in.
- A validation message appeared next to the Password field, requesting that it be filled in.
- The user remained on the Login page.

**Status:** PASS

---

### TC-LOGIN-03 — Login with incorrect credentials

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: `test@example.com`
- Password: `WrongPass123`

**Steps:**
1. Enter the email address in the Email Address field.
2. Enter the password in the Password field.
3. Click the Login button.

**Expected Result:**
- The user is not logged in.
- The application displays an error message indicating that the email or password is incorrect.
- The user remains on the Login page.

**Actual Result:**
- The user was not logged in.
- The application displayed the message: `Your email or password is incorrect!`
- The user remained on the Login page.

**Status:** PASS

---

### TC-LOGIN-04 — Login with registered email and incorrect password

**Preconditions:**
- The Login page is opened.
- A user account with the specified email address exists.

**Test Data:**
- Email Address: Registered test account email (redacted)
- Password: `DifferentPass456` (incorrect password)

**Steps:**
1. Enter the registered email address in the Email Address field.
2. Enter the incorrect password in the Password field.
3. Click the Login button.

**Expected Result:**
- The user is not logged in.
- The application displays an error message indicating that the email or password is incorrect.
- The user remains on the Login page.

**Actual Result:**
- The user was not logged in.
- The application displayed the message: `Your email or password is incorrect!`
- The user remained on the Login page.

**Status:** PASS

---

### TC-LOGIN-05 — Login with valid credentials

**Preconditions:**
- A registered user account exists.
- The Login page is opened.

**Test Data:**
- Email Address: Registered test account email (redacted)
- Password: Valid password (redacted)

**Steps:**
1. Enter the registered email address in the Email Address field.
2. Enter the correct password in the Password field.
3. Click the Login button.

**Expected Result:**
- The user is successfully logged in.
- The application redirects the user to the homepage.

**Actual Result:**
- The user was successfully logged in.
- The application redirected the user to the homepage.

**Status:** PASS

---

### TC-LOGIN-06 — Logout from the application

**Preconditions:**
- A registered user account exists.
- The user is logged in.
- The homepage is opened.

**Steps:**
1. Click the Logout button/link.
2. Observe the page displayed after clicking Logout.
3. Check whether the username is still displayed.
4. Check whether Login and Signup options are available.

**Expected Result:**
- The application redirects the user to the Login/Signup page.
- The username is no longer displayed.
- Login and Signup options are available.

**Actual Result:**
- The application redirected the user to the Login/Signup page.
- The username disappeared.
- Login and Signup options became available.

**Status:** PASS

**Note:** Only the UI behavior after logout was verified. Session termination was not tested.

---

### TC-LOGIN-07 — Verify Show/Hide Password functionality

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Password: `TestPass123`

**Steps:**
1. Enter a password into the Password field.
2. Click the eye icon.
3. Verify that the password is displayed as plain text.
4. Click the eye icon again.
5. Verify that the password is hidden.

**Expected Result:**
- The eye icon is displayed when the Password field contains text.
- Clicking the eye icon reveals the password.
- Clicking the eye icon again hides the password.

**Actual Result:**
- The eye icon was displayed when the Password field contained text.
- Clicking the eye icon revealed the password.
- Clicking the eye icon again hid the password.

**Status:** PASS

---

### TC-LOGIN-08 — Verify password visibility icon after losing focus

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Password: `TestPass123`

**Steps:**
1. Enter a password into the Password field.
2. Verify that the eye icon is displayed.
3. Click on an empty area outside the Password field.
4. Click on the Password field again.
5. Observe whether the eye icon is displayed.

**Expected Result:**
- The password is hidden after the Password field loses focus.
- The eye icon is available again when the user returns to the Password field, provided that the field still contains a password.

**Actual Result:**
- The password was hidden after the Password field lost focus.
- The eye icon disappeared and did not reappear when the user returned to the Password field.
- The eye icon became available again only after the password was cleared and entered again.

**Status:** FAIL

**Related bug:** BUG-LOGIN-01

---

## Test Execution Summary

| Result | Count |
|---|---:|
| PASS | 7 |
| FAIL | 1 |
| Total | 8 |

**Additional findings:**
- 1 confirmed UI defect (password visibility icon), documented in a separate bug report: BUG-LOGIN-01.

**Conclusion:** The Login module was tested for input validation, authentication with invalid and valid credentials, logout and password visibility behavior. The main issue identified concerns the password visibility icon disappearing after the Password field loses focus.