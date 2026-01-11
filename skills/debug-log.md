# Skill: Debug Logic & Error Analysis

> **Description:** Systematically analyze stack traces or error logs to identify root causes and propose fixes.
> **Outcome:** A diagnostic report with 3 potential fixes ranked by probability.
> **Measurable Value:** Reduces "time-to-fix" for bugs by ~50% (approx. 10-30 mins per bug).

## Instructions

When the user provides an error log or stack trace:

1.  **Isolate the Error:**
    - Identify the specific error type (e.g., `TypeError`, `500 Internal Server Error`).
    - Locate the file and line number in the user's project (ignore `node_modules`).

2.  **Contextual Analysis:**
    - Explain *why* this error typically happens (e.g., "Tried to access property of undefined").
    - If code context is provided, analyze the variable state.

3.  **Propose Solutions (Ranked):**
    - **Fix 1 (Most Likely):** The direct code correction.
    - **Fix 2 (Defensive):** How to prevent it (e.g., Optional Chaining `?.`).
    - **Fix 3 (Systemic):** A broader config or data-flow check.

## Example Prompt
"Debug this error: `Uncaught TypeError: Cannot read properties of undefined (reading 'map') at ProductList.tsx:12`"

## Example Output
### 🚨 Diagnosis
The array `products` is being accessed before it is initialized (it is likely `undefined` on the first render).

### 🛠️ Proposed Fixes

**1. Default Value (Immediate Fix)**
Initialize the state with an empty array instead of nothing.
```diff
- const [products, setProducts] = useState();
+ const [products, setProducts] = useState([]);
```

**2. Defensive Rendering (Safest)**
Use optional chaining or a guard clause in the JSX.
```tsx
{products?.map(item => ...)}
// OR
{products && products.length > 0 ? products.map(...) : <p>Loading...</p>}
```

**3. API Check (Root Cause)**
Ensure your API response actually returns an array and not an object wrapper (e.g., `{ data: [...] }`).
