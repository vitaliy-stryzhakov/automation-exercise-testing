# Products Module — Test Cases

**Project:** Automation Exercise  
**Module:** Products  
**Test type:** Manual Functional Testing  
**Test environment:** Windows, Microsoft Edge  
**Test status:** Completed

## Test Cases

### TC-PRODUCTS-01 — Verify the products list is displayed

**Preconditions:**
- The Home page is opened.

**Steps:**
1. Click the Products link in the header.
2. Observe the page content.

**Expected Result:**
The All Products page opens. Product cards are displayed with an image, price and name. Each card has an Add to cart button and a View Product link.

**Actual Result:**
The All Products page opened. Product cards were displayed with an image, price and name. Each card had an Add to cart button and a View Product link.

**Status:** PASS

---

### TC-PRODUCTS-02 — Verify product details page

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Click View Product on any product.
2. Check the product details.

**Expected Result:**
The product page displays name, category, price, availability, condition, brand and the Quantity field. The data matches the product card on the Products page.

**Actual Result:**
The product page displayed name, category, price, availability, condition, brand and the Quantity field. The data matched the product card on the Products page.

**Status:** PASS

---

### TC-PRODUCTS-03 — Add a product to the cart from the products list

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Hover over a product card.
2. Click Add to cart.
3. Check the confirmation message.
4. Open the Cart page.

**Expected Result:**
A confirmation message is displayed. The selected product is present in the cart.

**Actual Result:**
A confirmation message was displayed. The selected product was present in the cart.

**Status:** PASS

**Note:** This test verifies the Add to cart action on the Products page. Cart contents (name, price, quantity) are verified in detail in TC-CART-01.

---

### TC-PRODUCTS-04 — Add a product to the cart from the product details page

**Preconditions:**
- A product details page is opened.

**Test Data:**
- Quantity: `3`

**Steps:**
1. Enter the quantity in the Quantity field.
2. Click Add to cart.
3. Open the Cart page.

**Expected Result:**
The product is added to the cart with the quantity entered on the product details page (3).

**Actual Result:**
The product was added to the cart with quantity 3.

**Status:** PASS

**Note:** Subtotal calculation and quantity updates for existing items are verified in TC-CART-03 and TC-CART-09. Zero and negative quantities are covered by TC-CART-10 and BUG-CART-01.

---

### TC-PRODUCTS-05 — Verify Quantity field with non-numeric and decimal values

**Preconditions:**
- A product details page is opened.

**Test Data:**
- Quantity: `abc`, `1.5`, empty

**Steps:**
1. Enter the value in the Quantity field.
2. Click Add to cart.
3. Open the Cart page.
4. Repeat for each value.

**Expected Result:**
The application rejects invalid values or corrects them, and does not add a product with an invalid quantity.

**Actual Result:**
- `abc`: the field did not accept letters. The value could not be entered.
- `1.5`: the field accepted the value. After clicking Add to cart, the product was not added to the cart.
- Empty: the field was left empty. After clicking Add to cart, the product was not added to the cart.

**Status:** PASS

**Related bug:** BUG-CART-01

**Related test case:** TC-CART-10

**Note:** Letters were blocked at the input level, while `1.5` and the empty value were accepted by the field and rejected only after clicking Add to cart. Zero and negative quantities are tested in TC-CART-10, where the application behaves differently: they are accepted.

---

### TC-PRODUCTS-06 — Search for an existing product

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Search query: `Blue Top`

**Steps:**
1. Enter the query in the search field.
2. Click the search button.

**Expected Result:**
The Searched Products section is displayed. The results contain the matching product.

**Actual Result:**
The Searched Products section was displayed. The results contained the matching product.

**Status:** PASS

**Note:** Pressing Enter does not start the search. See UI-OBS-04.

---

### TC-PRODUCTS-07 — Search for a non-existent product

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Search query: `qwertyxyz`

**Steps:**
1. Enter the query in the search field.
2. Click the search button.

**Expected Result:**
No products are displayed. The application shows an understandable empty-result state without errors.

**Actual Result:**
No products were displayed. The application showed an understandable empty-result state without errors.

**Status:** PASS

---

### TC-PRODUCTS-08 — Search with an empty query

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Leave the search field empty.
2. Click the search button.

**Expected Result:**
The application does not break. The full product list is displayed.

**Actual Result:**
The application did not break. The full product list was displayed.

**Status:** PASS

---

### TC-PRODUCTS-09 — Search is case-insensitive

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Search query: `blue top`, `BLUE TOP`, `BlUe ToP`

**Steps:**
1. Enter each query in the search field.
2. Click the search button.
3. Compare the results.

**Expected Result:**
All queries return the same results.

**Actual Result:**
All queries returned the same results.

**Status:** PASS

---

### TC-PRODUCTS-10 — Search by partial name

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Search query: `top`

**Steps:**
1. Enter the query in the search field.
2. Click the search button.

**Expected Result:**
All products containing the entered text in their names are displayed.

**Actual Result:**
All products containing the entered text in their names were displayed.

**Status:** PASS

---

### TC-PRODUCTS-11 — Search with special characters

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Search query: `%`, `<script>`, `' OR 1=1`

**Steps:**
1. Enter each query in the search field.
2. Click the search button.

**Expected Result:**
The queries are processed as plain text. No errors, broken layout or script execution occurs.

**Actual Result:**
The queries were processed as plain text. No errors, broken layout or script execution occurred.

**Status:** PASS

**Note:** This is a basic input-handling check only. Security testing is out of scope.

---

### TC-PRODUCTS-12 — Filter products by category

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Expand a category in the sidebar (for example, Women).
2. Select a subcategory (for example, Tops).
3. Check the displayed products.

**Expected Result:**
The page title reflects the selected category. Only products from this category are displayed.

**Actual Result:**
The page title reflected the selected category. Only products from this category were displayed.

**Status:** PASS

---

### TC-PRODUCTS-13 — Filter products by brand

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Select a brand in the sidebar (for example, Polo).
2. Check the displayed products.

**Expected Result:**
The page title reflects the selected brand. Only products of this brand are displayed.

**Actual Result:**
The page title reflected the selected brand. Only products of this brand were displayed.

**Status:** PASS

---

### TC-PRODUCTS-14 — Switch between categories and brands

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Select a category.
2. Select a brand.
3. Select a different category.
4. Check the displayed products after each step.

**Expected Result:**
The product list updates correctly after each selection and does not keep products from the previous filter.

**Actual Result:**
The product list was updated correctly after each selection and did not keep products from the previous filter.

**Status:** PASS

---

### TC-PRODUCTS-15 — Submit a product review with valid data

**Preconditions:**
- The Products page is opened.

**Test Data:**
- Name: `Test User`
- Email: `test@example.com`
- Review: `Test review`

**Steps:**
1. Click View Product on any product.
2. Fill in the Name, Email and Review fields.
3. Click Submit.

**Expected Result:**
A success message is displayed.

**Actual Result:**
A success message was displayed.

**Status:** PASS

---

### TC-PRODUCTS-16 — Submit a product review with empty fields

**Preconditions:**
- A product details page is opened.

**Steps:**
1. Leave all review fields empty.
2. Click Submit.

**Expected Result:**
The review is not submitted. A validation message is displayed.

**Actual Result:**
The review was not submitted. A validation message appeared next to the Name field, requesting that it be filled in.

**Status:** PASS

---

### TC-PRODUCTS-17 — Submit a product review with an invalid email

**Preconditions:**
- A product details page is opened.

**Test Data:**
- Name: `Test User`
- Email: `test@`
- Review: `Test review`

**Steps:**
1. Fill in the fields using the test data.
2. Click Submit.

**Expected Result:**
The review is not submitted. A validation message about the email format is displayed.

**Actual Result:**
The review was not submitted. A validation message about the email format was displayed.

**Status:** PASS

---

### TC-PRODUCTS-18 — Verify product data consistency between list and details

**Preconditions:**
- The Products page is opened.

**Steps:**
1. Note the name and price of a product on the list.
2. Click View Product on the same product.
3. Compare the data.

**Expected Result:**
The name and price are identical on both pages.

**Actual Result:**
The name and price were identical on both pages.

**Status:** PASS

---

## UI Observations

These observations were identified during exploratory testing. They are not confirmed functional defects because formal UI requirements were not available.

### UI-OBS-01 — Hover overlay covers the product image

**Observation:**
When the cursor is placed over a product image on the Products page, a sliding overlay appears and covers the image. The user cannot click the image to open the product page.

**Impact:**
Users who try to open a product by clicking its image are blocked by the overlay, which makes navigation less intuitive.

**Suggestion:**
Make the overlay non-blocking, or make the product image clickable and lead to the product details page.

---

### UI-OBS-02 — Add to cart button and price are duplicated by the hover overlay

**Observation:**
Each product card shows an Add to cart button and a price. When the cursor is placed over the card, the overlay covers the original button and shows the same price and Add to cart button again.

**Impact:**
The duplicated elements are redundant, and the purpose of the original button is unclear because it is hidden as soon as the user tries to use it.

**Suggestion:**
Keep only one Add to cart button and one price on the card, or make the overlay show additional information instead of duplicating the existing one.

---

### UI-OBS-03 — Product page can be opened only through the View Product link

**Observation:**
The product details page can be opened only by clicking the small View Product link. Clicking the product image or the product name does not open it.

**Impact:**
The link is small compared to the image, and users expect to open a product by clicking its image. This makes navigation less convenient.

**Suggestion:**
Make the product image and name clickable and lead to the product details page.

---

### UI-OBS-04 — Search is not started by pressing Enter

**Observation:**
After entering a query in the search field, pressing Enter does not start the search. The search starts only after clicking the search button.

**Impact:**
Pressing Enter is a common way to submit a search, so users may think the search does not work.

**Suggestion:**
Allow starting the search by pressing Enter.

---

## Test Execution Summary

| Result | Count |
|---|---:|
| PASS | 18 |
| FAIL | 0 |
| Total | 18 |

**Additional findings:**
- No functional defects were found in the Products module.
- 4 UI observations recorded for further review.

**Conclusion:** The Products module was tested for product list and details display, adding products to the cart, quantity input, search, filtering by category and brand, product reviews and data consistency. No functional defects were identified. The main concerns relate to usability of the product cards, which are recorded as UI observations.