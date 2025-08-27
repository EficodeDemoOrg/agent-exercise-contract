# Digital Grade Checker – MVP Project Brief

## 1. The Client & The Challenge

**Scenario:**  
Our team is building a "Digital Grade Checker" for a construction technology client. The tool will provide machine operators with real-time, visual feedback to ensure their work matches digital construction plans.

**Goal:**  
Accelerate client feedback by developing the UI prototype and backend engine in parallel, using a [shared data contract](data/DATA_CONTRACT.md).

**Purpose of MVP:**  
- **UI Prototype:** Early client feedback on look and feel.
- **Backend Engine:** Prove robust, accurate calculation logic.

---

## 2. Two Parallel Development Paths

### Path A: Client-Facing UI Prototype (Frontend Focus)

- Build an interactive, single-page web app that simulates the operator’s in-cab experience.
- Use mocked data from the shared contract.
- **Features:**
  - Display "target grade" as a line.
  - Show excavator bucket as icon/dot based on input position.
  - Bucket color reflects status:  
    - Green: `on_grade`  
    - Yellow: `too_high`  
    - Red: `too_deep`
  - Show numerical vertical distance ("delta") to target grade.
  - Visualization updates instantly with new position data.

### Path B: Core Calculation Engine (Backend Focus)

- Build a standalone CLI tool implementing the business logic.
- **Features:**
  - Accept bucket position as command-line arguments (e.g., `--x=65 --y=15`).
  - Perform calculations per the shared Data Contract.
  - Print a well-formatted summary of the result to the console.

---

## 3. Shared Contract & Mock Data

- Both paths use a shared Data Contract for "Grade Check Result."
- Mock data for the digital plan and bucket position provided for testing.

---

## 4. Expected Outcome & Deliverables

- Functional MVP for chosen path.
- **Demo (5 min):**
  - Show how the prototype meets requirements.
  - Explain how your component accelerates client feedback.
  - Briefly describe your approach and tools used.

---

## 5. Stretch Goals (Optional)

- **Frontend:**  
  - Dynamic plan editing (drag points in UI).
  - Obstacle visualization (pipes/cables in cross-section).
- **Backend:**  
  - Support curved/multi-segment grade lines.
  - Tolerance configuration (`--tolerance=0.25` for "on_grade" status).
- **Full-Stack:**  
  - Integrate backend engine logic directly into the visualizer.

---

## 6. Learning Goals

- **Adopt an Agentic Workflow**: The primary goal is to practice building a complete prototype using an AI agent as your primary development partner.
- **Practice Thread Isolation**: Learn to manage complexity by assigning distinct, single-purpose tasks to separate, isolated agent threads.
- **Utilize AI for Planning**: Use the agent not just for coding, but as a strategic partner to create a project roadmap and a TODO.md to track progress.
- **Master Task Decomposition**: Break down the larger project goal into small, well-defined tasks that can be completed by a focused agent in a single thread.
- **Leverage Agent Personas**: Improve the quality of the AI's output by assigning it specific, expert roles (e.g., "You are a senior backend developer," "You are a UX expert specializing in SVG").

**Note:**  
Both components must strictly follow the shared Data Contract to ensure seamless integration and rapid feedback cycles.
