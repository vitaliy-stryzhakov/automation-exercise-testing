# Cart Module — Test Cases

**Project:** Automation Exercise  
**Module:** Cart  
**Test type:** Manual Functional Testing  
**Test environment:** Windows, Microsoft Edge  
**Test status:** Completed

## Test Cases

### TC-CART-01 — Add a single product to the cart

**Preconditions:**
- User is logged in.
- Cart is empty.

**Steps:**
1. Open the Products page.
2. Select a product.
3. Click Add to cart.
4. Open the Cart page.

**Expected Result:**
The selected product is displayed in the cart with the correct name, price and quantity (1).

**Actual Result:**
The product was added successfully. Name, price and quantity were displayed correctly.

**Status:** PASS

---

### TC-CART-02 — Add multiple products to the cart

**Preconditions:**
- User is logged in.
- Cart is empty.

**Steps:**
1. Open the Products page.
2. Add Blue Top to the cart.
3. Add Men Tshirt to the cart.
4. Open the Cart page.

**Expected Result:**
Both products are displayed with correct names, prices and quantities.

**Actual Result:**
Both products were displayed correctly. Their names and prices matched the selected products. Quantity was 1 for each product.

**Status:** PASS

---

### TC-CART-03 — Verify product subtotal calculation

**Preconditions:**
- Cart contains Blue Top and Men Tshirt.

**Test Data:**
- Blue Top: 500 × 2
- Men Tshirt: 400 × 1

**Steps:**
1. Set the Blue Top quantity to 2 on its product page and add it to the cart.
2. Open the Cart page.
3. Check the quantity and subtotal of each product.

**Expected Result:**
Each product subtotal is calculated as unit price multiplied by quantity.

**Actual Result:**
- Blue Top: 500 × 2 = 1000.
- Men Tshirt: 400 × 1 = 400.

Both subtotals were correct.

**Status:** PASS

---

### TC-CART-04 — Remove a product from the cart

**Preconditions:**
- Cart contains at least two products.

**Steps:**
1. Open the Cart page.
2. Locate one of the products.
3. Click its remove button.
4. Check the remaining products.

**Expected Result:**
The selected product is removed. Other products remain in the cart.

**Actual Result:**
The selected product was removed successfully. The other product remained in the cart.

**Status:** PASS

---

### TC-CART-05 — Verify empty cart state

**Preconditions:**
- Cart contains one product.

**Steps:**
1. Open the Cart page.
2. Remove the remaining product.
3. Check the displayed cart state.

**Expected Result:**
The cart displays an appropriate empty-state message. Products and checkout controls are no longer displayed.

**Actual Result:**
The message `Cart is empty! Click here to buy products` appeared. Products and the Proceed To Checkout button disappeared.

**Status:** PASS

---

### TC-CART-06 — Verify cart persistence after page refresh

**Preconditions:**
- Cart contains two products.

**Steps:**
1. Open the Cart page.
2. Refresh the page using F5.
3. Check the cart contents.

**Expected Result:**
Products, quantities and prices remain unchanged after refreshing the page.

**Actual Result:**
Both products remained in the cart. Quantities and prices were preserved.

**Status:** PASS

---

### TC-CART-07 — Verify cart persistence after navigating between pages

**Preconditions:**
- Cart contains two products.

**Steps:**
1. Open the Home page.
2. Navigate to the Products page.
3. Navigate to the Cart page.
4. Check the cart contents.

**Expected Result:**
Products remain in the cart after navigating between pages.

**Actual Result:**
Both products remained in the cart. Quantities and prices were preserved.

**Status:** PASS

---

### TC-CART-08 — Verify cart persistence after logout and login

**Preconditions:**
- User is logged in.
- Cart contains two products.

**Steps:**
1. Log out of the application.
2. Log in again using the same account.
3. Open the Cart page.
4. Check the cart contents.

**Expected Result:**
Previously added products remain in the cart after logging in again.

**Actual Result:**
Both products remained in the cart. Quantities and prices were preserved.

**Status:** PASS

---

### TC-CART-09 — Verify quantity update by adding an existing product again

**Preconditions:**
- Cart contains Blue Top with quantity 1.

**Steps:**
1. Open the Blue Top product page.
2. Set the quantity to 2.
3. Click Add to cart.
4. Open the Cart page.
5. Check the product quantity and subtotal.

**Expected Result:**
The quantity of the existing product is updated according to the amount added.

**Actual Result:**
The quantity became 3 (1 + 2). The subtotal was 1500.

**Status:** PASS

---

### TC-CART-10 — Verify product quantity validation

**Preconditions:**
- User is logged in.

**Test Data:**
- Quantity: `0`, `-1`

**Steps:**
1. Open a product page.
2. Manually enter 0 into the Quantity field.
3. Click Add to cart.
4. Check the cart.
5. Repeat the test using a negative quantity (-1).

**Expected Result:**
The application prevents adding products with zero or negative quantities.

**Actual Result:**
The application accepted both values. Products with quantities 0 and -1 were added to the cart. Their totals were calculated accordingly.

**Status:** FAIL

**Related bug:** BUG-CART-01

**Related test case:** TC-PRODUCTS-05

---

### TC-CART-11 — Verify cart behavior when adding a negative quantity to an existing product

**Preconditions:**
- Cart contains Blue Top with quantity 3.

**Test Data:**
- Quantity: `-5`

**Steps:**
1. Open the Blue Top product page.
2. Enter -5 into the Quantity field.
3. Click Add to cart.
4. Open the Cart page.
5. Check the product quantity and subtotal.

**Expected Result:**
The application prevents a negative quantity from being added.

**Actual Result:**
The quantity changed from 3 to -2. The subtotal became -1000.

**Status:** FAIL

**Related bug:** BUG-CART-01

---

### TC-CART-12 — Verify checkout with invalid product quantities

**Preconditions:**
- Cart contains products with zero and negative quantities.

**Steps:**
1. Open the Cart page.
2. Click Proceed To Checkout.
3. Check the products and their quantities on the checkout page.

**Expected Result:**
The application prevents checkout while invalid product quantities are present.

**Actual Result:**
The checkout page opened successfully. Products with zero and negative quantities remained in the order.

**Status:** FAIL

**Related bug:** BUG-CART-01

---

### TC-CART-13 — Verify order placement with invalid product quantities

**Preconditions:**
- Checkout page contains products with zero and negative quantities.

**Steps:**
1. Proceed to checkout with the invalid cart contents.
2. Leave the optional comment field empty.
3. Click Place Order.
4. Observe the next page.

**Expected Result:**
The application prevents proceeding with an order containing invalid product quantities.

**Actual Result:**
The payment form opened without an error. No payment details were entered and no payment was submitted.

**Status:** FAIL

**Related bug:** BUG-CART-01

**Note:** Partial coverage. The test verifies access to the payment form only. Successful payment or order placement was not tested.

---

### TC-CART-14 — Verify cart behavior when adding different products

**Preconditions:**
- User is logged in.
- Cart is empty.

**Steps:**
1. Add Blue Top to the cart.
2. Add Men Tshirt to the cart.
3. Add Sleeveless Dress to the cart.
4. Open the Cart page.
5. Check all products.

**Expected Result:**
All selected products are displayed separately with correct names, prices and quantities.

**Actual Result:**
All three products were displayed correctly with the expected names, prices and quantities.

**Status:** PASS

---

### TC-CART-15 — Verify cart behavior when navigating back from checkout

**Preconditions:**
- Cart contains two products.

**Steps:**
1. Open the Cart page.
2. Click Proceed To Checkout.
3. Use the browser Back button.
4. Check the cart contents.

**Expected Result:**
Previously added products and their quantities remain unchanged.

**Actual Result:**
Cart contents were preserved correctly after returning from checkout.

**Status:** PASS

---

### TC-CART-16 — Verify cart behavior after opening it in a new browser tab

**Preconditions:**
- Cart contains two products.
- The same browser session is active.

**Steps:**
1. Open the website in a new browser tab.
2. Navigate to the Cart page.
3. Check the cart contents.

**Expected Result:**
Products remain available in the cart in the new tab within the same browser session.

**Actual Result:**
Both products were displayed correctly.

**Status:** PASS

---

## UI Observations

These observations were identified during exploratory testing. They are not confirmed functional defects because formal UI requirements were not available.

### UI-OBS-01 — Remove button is difficult to discover

**Observation:**
The remove (X) button was visible only when hovering over a specific area near the end of the product row. Hovering directly over the product did not reveal it.

**Impact:**
Users may have difficulty discovering how to remove a product from the cart.

**Suggestion:**
Make the remove button consistently visible or easier to discover.

---

### UI-OBS-02 — Cart page does not display the overall order total

**Observation:**
The Cart page displayed individual product subtotals, but the overall order total was not visible there. The total was displayed later on the checkout page.

**Impact:**
Users cannot immediately see the combined cost of their cart before proceeding to checkout.

**Suggestion:**
Consider displaying the overall cart total on the Cart page.

---

## Test Execution Summary

| Result | Count |
|---|---:|
| PASS | 12 |
| FAIL | 4 |
| Total | 16 |

**Additional findings:**
- 1 confirmed validation issue involving zero and negative quantities, documented in a separate bug report: BUG-CART-01.
- 2 UI observations recorded for further review.

**Conclusion:** The Cart module was tested for product management, quantity handling, subtotal calculation, persistence, navigation and checkout behavior. The main issue identified concerns the acceptance and propagation of invalid product quantities.