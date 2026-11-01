# Deadlock Analysis and Resource Allocation Dashboard

An interactive, pure-client-side simulation and visualization dashboard for core Operating Systems deadlock handling algorithms. This suite provides visual tools, empirical test suites, and step-by-step traces for **Deadlock Avoidance** (Banker's Algorithm), **Deadlock Detection** (Resource Allocation Graph & Vector Reduction), **Deadlock Recovery** (Process Termination), and **Deadlock Prevention** (Coffman Condition Elimination).

---

## 📌 Project Overview

Deadlocks represent a fundamental challenge in multitasking operating systems when concurrent processes compete for finite resources. This dashboard provides an educational, interactive laboratory to inspect system states, test hypothetical resource requests, identify permanent blocking conditions, and observe policy-based prevention strategies in real time.

---

## 🚀 Main Features

- **Deadlock Avoidance (Banker's Algorithm)**:
  - Real-time safety algorithm evaluation calculating dynamic $\text{Work}$ and $\text{Need} = \text{Max} - \text{Allocation}$ matrices.
  - Generates verified safe execution sequences (e.g., $P_1 \to P_3 \to P_4 \to P_0 \to P_2$).
  - Speculative request testing with immediate validation: granted, waiting (deferred), or denied (unsafe).
- **Deadlock Detection**:
  - **Single-Instance Resources**: Cycle detection on directed bipartite Resource-Allocation Graphs (Wait-For Graph) using Depth-First Search (DFS).
  - **Multiple-Instance Resources**: Matrix reduction algorithm identifying processes that can never complete given current Available resources and pending requests.
  - Interactive SVG Resource-Allocation Graph visualization with active node and arrow statuses.
- **Deadlock Recovery**:
  - Interactive victim selection and process termination.
  - Automated resource reclamation releasing all held resources back to the Available pool.
  - Post-recovery system re-evaluation confirming whether deadlock has been resolved.
- **Deadlock Prevention**:
  - Discrete event execution simulator evaluating how processes acquire resources over time.
  - Eliminates **Circular Wait** via Hierarchical Resource Ordering ($A \to B \to C$).
  - Eliminates **Hold and Wait** via All-or-Nothing simultaneous resource acquisition.
  - Tick-by-tick timeline comparison against unconstrained baseline execution.
- **Automated Test Suite (TC1–TC6)**:
  - Built-in analytical test runner verifying standard textbook scenarios, deadlock conditions, prevention policies, and input validation boundaries.

---

## 🛠️ Technologies Used

- **HTML5**: Semantic document layout with accessible ARIA tabpanel navigation.
- **CSS3**: Modern dark-theme UI with responsive CSS Grid, Flexbox, custom design tokens, and smooth status transitions.
- **JavaScript (ES6+)**: Pure functional algorithms without external dependencies or heavy frameworks.
- **SVG**: Dynamic mathematical rendering of directed Resource-Allocation Graphs and Wait-For cycles.

---

## 📂 Project Structure

```
deadlock-analysis-dashboard/
├── css/
│   └── styles.css          # Dark theme styles, responsive layout & graph styling
├── js/
│   ├── app.js              # UI controller, event listeners, and SVG graph renderer
│   ├── engine.js           # Core algorithms: Banker's safety, detection, recovery & prevention
│   ├── presets.js          # Standard configurations & edge-case presets
│   └── cases.js            # Analytical test case definitions (TC1–TC6)
├── tests/
│   └── run_tests.js        # Automated test suite (CommonJS / Node.js compatible)
├── .gitignore              # Ignored system, editor, and build artifacts
├── AI_Usage_Record.md      # AI usage and verification documentation
├── index.html              # Main dashboard user interface
├── README.md               # Project documentation
└── Test_Case_Analysis.md   # Analytical test results and TC6 breakdown
```

---

## 💻 Instructions to Run the Project Locally

Because the dashboard is built with vanilla HTML, CSS, and JavaScript, no complex installation, build steps, or external packages are required.

### Option 1: Run with Python (Recommended)

1. Open a terminal or command prompt in the project root directory.
2. Start Python's built-in HTTP server:
   ```bash
   python -m http.server 8000
   ```
3. Open your browser and navigate to:
   ```
   http://localhost:8000
   ```

### Option 2: Run with Node.js (`npx serve`)

```bash
npx serve .
```

### Option 3: Direct File Execution

Double-click `index.html` or open it directly in any modern web browser (Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari).

---

## 📖 How to Use the Dashboard

1. **Avoidance Tab**:
   - Choose a preset or set custom process/resource counts and click **Apply size**.
   - Edit values directly in the **Allocation**, **Maximum**, or **Available** matrix tables.
   - Click **Run safety check** to view the safety status, safe sequence, and step-by-step Work vector updates.
   - Under **Resource request**, specify a process (e.g., `P1`) and a request vector (e.g., `1 0 2`), then click **Submit request** to simulate hypothetical allocation.
2. **Detection Tab**:
   - Load single-instance or multiple-instance scenarios from the dropdown.
   - Click **Run detection** to analyze the current system state.
   - Inspect the generated Resource-Allocation Graph, circular wait detection, and deadlocked processes.
3. **Recovery Tab**:
   - When a deadlocked scenario is active, navigate to the **Recovery** tab.
   - Select a candidate process to terminate from the dropdown and review the resource reclamation preview.
   - Click **Terminate and release resources** to observe how released resources allow remaining processes to resume execution.
4. **Prevention Tab**:
   - View the resource acquisition order for active processes.
   - Switch between **No policy**, **Resource ordering**, and **All-or-nothing** radio options.
   - Review the policy comparison table and tick-by-tick timeline explaining trade-offs in concurrency and waiting time.
5. **Test Cases Tab**:
   - Click **Run all test cases** to execute the complete verification suite directly in the browser and inspect the analytical evaluation breakdown.

---

## 🔍 Modules Explanation

| Module | OS Principle | Core Algorithm / Mechanism |
|---|---|---|
| **Deadlock Avoidance** | Safe vs. Unsafe States | **Banker's Algorithm**: Checks if speculative allocation leaves at least one execution sequence where $\text{Need} \le \text{Work}$. |
| **Deadlock Detection** | Wait-For Dependencies | **DFS Cycle Detection** (Single-Instance) and **Matrix Reduction** (Multiple-Instance): Identifies permanently blocked threads. |
| **Deadlock Recovery** | Resource Reclamation | **Process Termination**: Reclaims allocated resources to the system Available pool until all remaining processes complete. |
| **Deadlock Prevention** | Coffman Conditions | **Hierarchical Ordering** (negates Circular Wait) and **Simultaneous Hold** (negates Hold-and-Wait). |

---

## 🧪 Automated Testing

To run the automated engine test suite via command line (Node.js):

```bash
node tests/run_tests.js
```

All 15 test groups verify:
- Accurate calculation of the Need matrix ($\text{Need} = \text{Max} - \text{Allocation}$).
- Exact reproduction of textbook safe sequence derivations.
- Proper request classification (safe grant, deferred waiting, unsafe rejection, and invalid input rejection).
- Exhaustive verification against permutation search over 300 randomized states.
