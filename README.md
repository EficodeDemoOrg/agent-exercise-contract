# Digital Grade Checker – MVP Project Brief

## 1. The Client & The Challenge

**Scenario:**  
Our team is building a "Digital Grade Checker" for a construction technology client. The tool will provide machine operators with real-time, visual feedback to ensure their work matches digital construction plans.

**Goal:**  
Accelerate client feedback by developing the UI prototype and backend engine in parallel, using a [shared data contract](docs/DATA_CONTRACT.md).

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
 
### Concept: A Simple 2D Visualizer
To help you get started, think of the app as a simple 2D side-view graph representing a cross-section of the ground.

- The Look: The interface will have a main canvas area. On this canvas, you'll draw a fixed "target grade" line. The "excavator bucket" will be a dot or icon whose position is controlled by the user. Next to the canvas, a text area will display the "delta" (the vertical distance to the line).

- The Interaction: The user will need input controls (like two text boxes or sliders) to change the bucket's X (horizontal) and Y (vertical) position. When they change these values, the app should react instantly:

  - The bucket dot moves to the new location on the canvas.

  - The application recalculates if the bucket is too high, too deep, or on grade.

  - The dot's color changes accordingly, and the delta text updates with the new distance.

This creates a simple, real-time feedback loop, simulating what an operator would see on their dashboard.

### Path B: Core Calculation Engine (Backend Focus)

- Build a standalone CLI tool implementing the business logic.
- **Features:**
  - Accept bucket position as command-line arguments (e.g., `--x=65 --y=15`).
  - Perform calculations per the shared Data Contract.
  - Print a well-formatted summary of the result to the console.
 
### Concept: A Simple Command-Line Engine
Think of this tool as a non-visual calculator. It doesn't have a graphical interface; all interaction happens through text commands in a terminal. Its single job is to take position data as input, calculate the result, and print a clear, human-readable summary.

How it Works: A user will run your program from their terminal, providing the bucket's coordinates as arguments directly in the command. The program will then execute, perform its logic, print the output, and exit.

Example Command: The user would type something like this into their terminal to run your tool:

```Bash

# For a Node.js script
node check-grade.js --x=65 --y=15.2

# Or for a Python script
python grade_checker.py --x=65 --y=15.2
Example Console Output: After running the command, the program should print a clean summary to the console. This is your "well-formatted summary." For example:

--- Grade Check Result ---
Status:           too_deep
Bucket Position:  (x: 65, y: 15.2)
Target Grade:     14.92m at this position
Delta:            -0.28m
--------------------------
```

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
- **Practice Blueprint Creation**: Start new projects by collaborating with an AI Architect to establish foundational technical decisions before implementation.
- **Practice Thread Isolation**: Learn to manage complexity by assigning distinct, single-purpose tasks to separate, isolated agent threads.
- **Utilize AI for Planning**: Use the agent not just for coding, but as a strategic partner to create a project roadmap and a TODO.md to track progress.
- **Task Decomposition**: Break down the larger project goal into small, well-defined tasks that can be completed by a focused agent in a single thread.
- **Practice Memory Persistence Between Agent Threads**: Utilize persisting markdown files in a systematic way to ground agents in a shared 'memory'.
- **Leverage Agent Roles**: Improve the quality of the AI's output by assigning it specific, expert roles (e.g., "You are a senior backend developer," "You are a UX expert specializing in SVG").

**Note:**  
For the Digital Grade Checker project, both components must strictly follow the shared Data Contract to ensure seamless integration and rapid feedback cycles. For the Context Window Visualizer, focus on the internal state model and real-time visualization requirements.
