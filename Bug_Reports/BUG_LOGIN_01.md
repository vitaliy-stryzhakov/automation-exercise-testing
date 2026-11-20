# BUG-LOGIN-01 — Password visibility icon disappears after the Password field loses focus

**Project:** Automation Exercise  
**Module:** Login  
**Severity:** Minor (provisional)  
**Priority:** Low (provisional)  
**Status:** New  
**Environment:** Windows, Microsoft Edge  
**Related test case:** TC-LOGIN-08

## Description

The eye icon used to show or hide the password disappears after the Password field loses focus. It does not reappear when the user clicks the field again, even though the field still contains a password.

The icon becomes available again only after the password is cleared and entered again.

## Preconditions

- The Login page is opened.

## Steps to Reproduce

1. Enter any password into the Password field.
2. Verify that the eye icon is displayed.
3. Click on an empty area of the page outside the Password field.
4. Click on the Password field again.
5. Observe the eye icon.

## Expected Result

The eye icon remains available or reappears when the user returns to the Password field, as long as the field contains a password.

## Actual Result

The eye icon disappears after the Password field loses focus and does not reappear when the user clicks the field again. It appears only after the password is cleared and entered again.

## Severity and Priority Notes

Severity and priority are provisional because formal requirements for the Show/Hide Password feature were not available during testing.

The issue does not block login, but it reduces usability: the user cannot verify a previously entered password without retyping it.