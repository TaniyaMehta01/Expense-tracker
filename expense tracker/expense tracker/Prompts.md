# Prompts & AI Development Log — Sprint 02 Cash-Flow Module

This document logs the engineering prompts, iterative requirements breakdown, and AI pairing workflow used to develop the **Cash-Flow (Salary & Expense Tracker Module)** for Sprint 02 on `workspace.prodesk.in`.

---

## 📌 Sprint 02 Scope & Objective
**Project**: "Cash-Flow" (Salary & Expense Tracker Module)  
**Objective**: Build a functional dashboard where a user can input their salary, log expenses, and view real-time state updates with threshold warnings, data persistence, dynamic charts, currency conversions, and PDF reports.

---

## 🛠️ Phased Prompts & Implementation Log

### Phase 1: Base MVP (Mandatory Deliverables - P0)
> **Prompt Instruction**:  
> "Implement the input architecture and core calculation logic:
> 1. Form capturing 'Total Salary' (Number), 'Expense Name' (Text), and 'Expense Amount' (Number).
> 2. Render Total Salary on the DOM upon submission.
> 3. Render new expenses dynamically to a list.
> 4. State formula: `Total Salary - Total Expenses = Remaining Balance`.
> 5. Validate all inputs: prevent execution and display error state if inputs are empty, zero, or negative.
> 6. Enforce strict numeric addition using `Number()` / `parseFloat()` so that numbers are never concatenated as strings (e.g., `10 + 10 = 20`, never `'1010'`)."

**Outcomes**:
- Implemented `#salary-form` and `#expense-form`.
- Bound numeric parsing avoiding concatenation.
- Displayed real-time metrics for Total Salary, Total Expenses, and Remaining Balance.

---

### Phase 2: Data Persistence & Visualization (Priority 1 Features)
> **Prompt Instruction**:  
> "Implement persistent browser storage and Chart.js visualization:
> 1. LocalStorage Integration: Serialize and save both Salary (`sprint02_salary`) and Expenses (`sprint02_expenses`) to `localStorage`. On page load, retrieve and render.
> 2. Delete Operations: Add a delete action with a Trash icon for each expense. Ensure clicking it removes the item from the DOM, updates `localStorage`, and recalculates the Remaining Balance instantly.
> 3. Data Visualization: Integrate Chart.js via CDN to render a dynamic Pie/Doughnut Chart displaying 'Remaining Balance vs. Total Expenses'. Properly handle `.destroy()` or `.update()` to eliminate duplicate canvas errors."

**Outcomes**:
- Created resilient storage methods `saveSalary()`, `loadSalary()`, `saveExpenses()`, `loadExpenses()`.
- Created Trash icon delete button recalculating balances instantaneously.
- Built Chart.js visualization with toggle between "Balance vs. Expenses" and "Category Breakdown".

---

### Phase 3: Stretch Goals & External APIs (Priority 2 Features)
> **Prompt Instruction**:  
> "Execute the high-performance stretch features:
> 1. Report Generation: Implement a 'Download Report (PDF)' button using jsPDF and AutoTable to export Total Salary, Total Expenses, Remaining Balance, and the itemized expense list.
> 2. Currency Conversion: Integrate Frankfurter API (`https://api.frankfurter.dev/v1/latest` with fallback to `https://api.frankfurter.app/latest`) to allow users to convert amounts between USD, INR, EUR, GBP, etc. in real-time.
> 3. Threshold Alerts: When Remaining Balance drops below 10% of Total Salary, trigger a critical UI warning (turn the balance text RED with `.text-danger-warning` and display `#threshold-alert-banner`)."

**Outcomes**:
- Configured threshold alert banner displaying dynamically whenever `remainingBalance < (totalSalary * 0.10)`.
- Implemented real-time currency converter with live Frankfurter exchange rates.
- Generated formatted PDF financial reports with jsPDF.

---

## 🧪 Technical FAQ Verification

1. **Numeric Concatenation (FAQ 1)**: Verified that amounts are parsed through `Number()`. `10 + 10 = 20`.
2. **`[object Object]` Prevention (FAQ 2)**: Verified `JSON.stringify()` on set, `JSON.parse()` on get.
3. **Vanilla JS Compliance (FAQ 3)**: Zero UI frameworks (React/Vue/Angular) used. Pure DOM manipulation.
4. **Chart.js CDN Lifecycle (FAQ 4 & 8)**: Loaded via CDN `<script>` tag. Single instance managed with `.destroy()` / `.update()`.
5. **Keyless Currency Endpoint (FAQ 7)**: Live keyless requests to Frankfurter API without paid keys.
