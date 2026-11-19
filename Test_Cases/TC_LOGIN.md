# TC-LOGIN-01 — Login with empty email and password

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: Empty
- Password: Empty

**Test Steps:**
1. Leave the Email Address field empty.
2. Leave the Password field empty.
3. Click the Login button.

**Expected Result:**
1. The user is not logged in.
2. A validation message indicates that the Email Address field is required.
3. The user remains on the Login page.

**Actual Result:**
1. The user is not logged in.
2. A validation message appears next to the Email Address field, requesting that it be filled in.
3. The user remains on the Login page.

**Status:** PASS


---

# TC-LOGIN-02 — Login with valid email and empty password

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: `test@example.com`
- Password: Empty

**Test Steps:**
1. Enter the email address in the Email Address field.
2. Leave the Password field empty.
3. Click the Login button.

**Expected Result:**
1. The user is not logged in.
2. A validation message indicates that the Password field is required.
3. The user remains on the Login page.

**Actual Result:**
1. The user is not logged in.
2. A validation message appears next to the Password field, requesting that it be filled in.
3. The user remains on the Login page.

**Status:** PASS


---

# TC-LOGIN-03 — Login with incorrect credentials

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Email Address: `test@example.com`
- Password: `WrongPass123`

**Test Steps:**
1. Enter the email address in the Email Address field.
2. Enter the password in the Password field.
3. Click the Login button.

**Expected Result:**
1. The user is not logged in.
2. The application displays an error message indicating that the email or password is incorrect.
3. The user remains on the Login page.

**Actual Result:**
1. The user is not logged in.
2. The application displays the message: `Your email or password is incorrect!`
3. The user remains on the Login page.

**Status:** PASS


---

# TC-LOGIN-04 — Login with registered email and incorrect password

**Preconditions:**
- The Login page is opened.
- A user account with the specified email address exists.

**Test Data:**
- Email Address: Registered test account email (redacted).
- Password: `DifferentPass456` (incorrect password).

**Test Steps:**
1. Enter the registered email address in the Email Address field.
2. Enter the incorrect password in the Password field.
3. Click the Login button.

**Expected Result:**
1. The user is not logged in.
2. The application displays an error message indicating that the email or password is incorrect.
3. The user remains on the Login page.

**Actual Result:**
1. The user is not logged in.
2. The application displays the message: `Your email or password is incorrect!`
3. The user remains on the Login page.

**Status:** PASS


---

# TC-LOGIN-05 — Login with valid credentials

**Preconditions:**
- A registered user account exists.
- The Login page is opened.

**Test Data:**
- Email Address: Registered test account email (redacted).
- Password: Valid password (redacted).

**Test Steps:**
1. Enter the registered email address in the Email Address field.
2. Enter the correct password in the Password field.
3. Click the Login button.

**Expected Result:**
1. The user is successfully logged in.
2. The application redirects the user to the homepage.

**Actual Result:**
1. The user is successfully logged in.
2. The application redirects the user to the homepage.

**Status:** PASS


---

# TC-LOGIN-06 — Logout from the application

**Preconditions:**
- A registered user account exists.
- The user is logged in.
- The homepage is opened.

**Test Data:**
- None.

**Test Steps:**
1. Click the Logout button/link.
2. Observe the page displayed after clicking Logout.
3. Check whether the username is still displayed.
4. Check whether Login and Signup options are available.

**Expected Result:**
1. The application redirects the user to the Login/Signup page.
2. The username is no longer displayed.
3. Login and Signup options are available.

**Actual Result:**
1. The application redirects the user to the Login/Signup page.
2. The username disappears.
3. Login and Signup options become available.

**Status:** PASS (UI behavior)


---

# TC-LOGIN-07 — Verify Show/Hide Password functionality

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Password: `TestPass123`

**Test Steps:**
1. Enter a password into the Password field.
2. Click the eye icon.
3. Verify that the password is displayed as plain text.
4. Click the eye icon again.
5. Verify that the password is hidden.

**Expected Result:**
1. The eye icon is displayed when the Password field contains text.
2. Clicking the eye icon reveals the password.
3. Clicking the eye icon again hides the password.

**Actual Result:**
1. The eye icon is displayed when the Password field contains text.
2. Clicking the eye icon reveals the password.
3. Clicking the eye icon again hides the password.

**Status:** PASS


---

# TC-LOGIN-08 — Verify password visibility icon after losing focus

**Preconditions:**
- The Login page is opened.

**Test Data:**
- Password: `TestPass123`

**Test Steps:**
1. Enter a password into the Password field.
2. Verify that the eye icon is displayed.
3. Click on an empty area outside the Password field.
4. Click on the Password field again.
5. Observe whether the eye icon is displayed.

**Expected Result:**
1. The password is hidden after the Password field loses focus.
2. The eye icon is available again when the user returns to the Password field, provided that the field still contains a password.

**Actual Result:**
1. The password is hidden after the Password field loses focus.
2. The eye icon disappears.
3. The eye icon does not reappear when the user returns to the Password field.
4. The eye icon becomes available again only after the password is cleared and entered again.

**Status:** FAIL