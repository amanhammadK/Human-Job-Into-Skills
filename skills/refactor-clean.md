# Skill: Refactor to Cleanup

> **Description:** Applying Clean Code principles (SOLID, DRY) to legacy or messy functions.
> **Outcome:** A Refactored version of the code that is more readable, testable, and maintainable.
> **Measurable Value:** Improves code quality metrics (Complexity) and saves ~20-30 mins of manual refactoring per file.

## Instructions

When the user asks to "clean up" or "refactor" a block of code:

1.  **Analyze Smells:**
    - Look for long functions (>20 lines).
    - Identify magic numbers/strings.
    - Spot nested conditionals (Arrow Code).
    - Find duplicated logic (DRY violations).

2.  **Refactoring Actions:**
    - **Extract Methods:** Break big functions into small, named utility functions.
    - **Guard Clauses:** Replace nested `if/else` with early returns.
    - **Typos/Naming:** Rename variables to be descriptive (e.g., `d` -> `days`).

3.  **Strict Output Format:**
    - Show the **Refactored Code** block first.
    - Provide a bulleted list of "Changes Made" below it.

## Example Prompt
"Refactor this nested spaghetti code for calculating order totals."

## Example Output
```javascript
// Refactored: distinct steps for readability
const calculateOrderTotal = (order) => {
  if (!order || order.items.length === 0) return 0; // Guard Clause

  const subtotal = order.items.reduce((acc, item) => acc + item.price, 0);
  const tax = calculateTax(subtotal, order.state);
  const shipping = shouldApplyShipping(subtotal) ? 10 : 0;

  return subtotal + tax + shipping;
};

// Extracted helpers for clarity
const calculateTax = (amount, state) => {
  const TAX_RATES = { 'CA': 0.1, 'NY': 0.08 }; // No magic numbers
  return amount * (TAX_RATES[state] || 0);
};

const shouldApplyShipping = (amount) => amount < 100;
```

**Changes Made:**
*   Introduced Guard Clause for empty orders.
*   Extracted `calculateTax` logic and removed magic numbers.
*   Simplified shipping logic into `shouldApplyShipping`.
