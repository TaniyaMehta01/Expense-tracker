# Cash-Flow — Salary & Expense Tracker Module
> **Sprint 02 Deliverable** &bull; Portal: `workspace.prodesk.in` &bull; Vanilla JavaScript, HTML5 & CSS3

**Cash-Flow** is a responsive, client-side personal finance dashboard engineered to help users manage monthly salary, log and manage expenses, observe real-time budget balances, monitor critical threshold alerts, visualize balance distributions with Chart.js, perform live currency conversions with Frankfurter API, and export downloadable PDF financial reports with jsPDF.

---

## 📋 Phased Requirements & Engineering Checklist

Based on the official **Sprint 02 Assignment Brief ("Cash-Flow")**:

### Phase 1: Base MVP (Mandatory Deliverables — P0)
- [x] **Input Architecture**: Form capturing `Total Salary` (Number), `Expense Name` (Text), and `Expense Amount` (Number) with strict numeric validation.
- [x] **State Logic**:
  - Renders **Total Salary** on the DOM upon submission.
  - Renders new expenses to a dynamic list.
  - Calculates and displays: **`Total Salary - Total Expenses = Remaining Balance`**.
  - **Active Currency Selector**: Choose base currency (USD `$`, INR `₹`, EUR `€`, GBP `£`, JPY `¥`, CAD `CA$`, AUD `A$`) directly alongside the Salary input, dynamically updating input symbols, dashboard metrics, and live rate conversions.
- [x] **Validation**: Prevents execution and displays error state if inputs are empty, zero, negative, or NaN.

### Phase 2: Data Persistence & Visualization (Priority 1 Features)
- [x] **LocalStorage Integration**: Persists across browser reloads. Serializes and saves both **Salary** (`sprint02_salary`) and **Expense Array** (`sprint02_expenses`) to the browser's `localStorage`. Retrieves and renders data on page load.
- [x] **Delete Operations**: Delete action with **Trash icon** for each expense. Removes item from DOM, updates `localStorage`, and recalculates Remaining Balance instantly.
- [x] **Data Visualization**: Dynamic **Chart.js Pie/Doughnut Chart** displaying **"Remaining Balance vs. Total Expenses"** (with toggle for Category distribution). Reuses or destroys chart instances properly to prevent duplicated canvases.

### Phase 3: Stretch Goals & External APIs (Priority 2 Features)
- [x] **Report Generation**: "Download Report" feature using **jsPDF** and **AutoTable** to export the expense list, total salary, total expenses, and final remaining balance as a formatted PDF.
- [x] **Currency Conversion (API)**: Real-time currency exchange using the keyless **Frankfurter API** (`https://api.frankfurter.dev/v1/latest` and `https://api.frankfurter.app/latest`) allowing users to convert currencies (e.g., INR to USD, USD to INR).
- [x] **Threshold Alerts**: If **"Remaining Balance" drops below 10% of Total Salary**, triggers a critical UI warning:
  - Turns the Remaining Balance text **RED** (`.text-danger-warning`).
  - Displays a prominent **Alert Banner** (`#threshold-alert-banner`).

---

## 🛠️ Non-Negotiable Technical Constraints

| Constraint | Implementation Detail | Status |
| :--- | :--- | :---: |
| **Vanilla JavaScript Only** | Zero React, Vue, or Angular. Manual DOM manipulation via `document.getElementById()`, `addEventListener()`, `textContent`. | ✅ PASS |
| **Strict Numeric Addition** | Number parsing via `Number()` / `parseFloat()` prevents string concatenation (`10 + 10 = 20`, never `"1010"`). | ✅ PASS |
| **LocalStorage Safety** | Safe serialization via `JSON.stringify()` / `JSON.parse()`. Corrupt data handled gracefully without crash. Never stores `[object Object]`. | ✅ PASS |
| **Chart.js Lifecycle** | Loaded via CDN `<script>` tag. Maintains single instance `expenseChart`. Destroys previous instance or mutates via `.update()`. | ✅ PASS |
| **Free Currency API** | Free/keyless endpoint Frankfurter API. No paid keys or payment secrets required. | ✅ PASS |
| **jsPDF Report** | Loaded via CDN `<script>`. Generates cleanly formatted A4 report. | ✅ PASS |

---

## 🚀 How to Run Locally

### Direct Browser Launch
Open `index.html` directly in your browser:
```bash
# Windows
start index.html

# Mac
open index.html
```

### Simple Static Server
```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```
Navigate to `http://localhost:8000`.

---

## 📂 Project Structure

```text
Taniya/
├── index.html          # Semantic HTML layout, salary bar, KPI cards, chart, converter, table
├── styles.css          # Design system, dark/light theme, alert banner, responsive layout
├── script.js           # Cash-flow state logic, math calculations, chart lifecycle, APIs
├── README.md           # Documentation, run instructions, requirements checklist
├── Prompts.md          # Development prompts log & AI pairing record
└── implementation.md   # Sprint 02 specification & non-negotiable guidelines
```
