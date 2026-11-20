# BUG-CART-01 — Application accepts zero and negative product quantities

**Project:** Automation Exercise  
**Module:** Cart  
**Severity:** Major (provisional)  
**Priority:** High (provisional)  
**Status:** New  
**Environment:** Windows, Microsoft Edge  
**Related test cases:** TC-CART-10, TC-CART-11, TC-CART-12, TC-CART-13

## Description

The application allows users to enter zero or negative values in the product Quantity field and add such products to the cart.

As a result, the cart displays invalid product quantities and calculates incorrect subtotals, including negative amounts.

## Preconditions

- User is logged in.
- Products page is accessible.

## Steps to Reproduce

### Scenario 1 — Zero quantity

1. Open the Products page.
2. Select a product.
3. Enter 0 in the Quantity field.
4. Click Add to cart.
5. Open the Cart page.

### Scenario 2 — Negative quantity

1. Open the Products page.
2. Select a product.
3. Enter -1 in the Quantity field.
4. Click Add to cart.
5. Open the Cart page.

## Expected Result

The application rejects zero and negative quantities and prevents such products from being added to the cart.

## Actual Result

The application accepts both values and adds the products to the cart.

- A product with quantity 0 is displayed with a total of 0.
- A product with quantity -1 is displayed with a negative total.

Further testing showed that negative quantities can also affect existing cart items and are preserved during checkout.

## Additional Evidence

- Adding a quantity of -5 to an existing Blue Top quantity of 3 resulted in a cart quantity of -2.
- The resulting subtotal was -1000.
- The checkout page accepted the cart with invalid quantities.
- Clicking Place Order opened the payment form.

**Note:** No payment details were entered and no payment was submitted.

## Severity and Priority Notes

Severity and priority are provisional because formal business requirements and the application's expected validation rules were not available during testing.

The issue may have a significant impact on order calculations and checkout integrity.