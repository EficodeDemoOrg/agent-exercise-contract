# Workshop Guidance: Agentic Workflow

## Objective
Build the "Digital Grade Checker" MVP from scratch by orchestrating a team of specialized AI agents. This guide outlines a structured workflow to manage context, ensure high-level output, and practice a modern, human-led AI development process.

## Why This Approach?

This workflow builds habits for effective AI collaboration by reinforcing good human practices: breaking problems into manageable pieces, maintaining focus, and taking strategic pauses instead of frantically forcing solutions.

**Context Management:** AI tools have limited context. This prevents "overflow" by having each agent level "zoom in" - Architect sees big picture, Lead Developer handles task relationships, Implementer focuses on specific code.

**Decision Hierarchy:** 
- **Architect** (Strategic): "What technology choices support our goals?"
- **Lead Developer** (Operational): "How do we sequence and organize tasks?"
- **Implementer** (Tactical): "How do I write this specific function?"

**Smart Escalation:** When conflicts exceed an agent's level (e.g., "This breaks tests elsewhere"), escalate up rather than making architectural decisions at the wrong level.

**Thread Isolation:** One conversation per domain/task. Use **Thread Dump** prompt (`.github/prompts/Thread Dump.prompt.md`) to transfer context when needed.

This prevents common pitfalls: jumping between tasks, mixing contexts, and losing track of what the AI is doing. The key principle is **deliberate context isolation** that supports both human understanding and AI effectiveness.

---shop Guidance: Agentic Workflow

## Objective
Build the "Digital Grade Checker" MVP from scratch by orchestrating a team of specialized AI agents. This guide outlines a structured workflow to manage context, ensure high-quality output, and practice a modern, human-led AI development process.

---

**Tooling Note:** Personas and prompts are available in the repository. The way you use them differs between tools.

**Personas (Agent Modes):** For Copilot, these are defined in `.github/chatmodes`. Cursor's "Custom Modes" are configured within the tool and are not directly visible in the project files. For Cursor it is possible to copy the content of these files and include the instructions into the custom mode.

**Reusable Prompts:** Copilot uses `.github/prompts`. For Cursor, you can create a local `.cursor/prompts` folder and @-reference the files.

## Phase 1: Architect (Ideation & High-Level Planning)

**Goal:**  
Define the project's technical direction and create foundational architecture documentation that guides implementation.ß

### Expected Deliverables

The Architect should produce these specific documents to establish the implementation structure:

- **`docs/system-architecture.md`** - High-level system design, component relationships, and tech stack decisions with rationale
- **`docs/data-contract-validation.md`** - Confirms existing DATA_CONTRACT.md is sufficient or extends it with additional requirements
- **`docs/implementation-structure.md`** - Proposed folder structure, module boundaries, and file organization
- **`TODO.md`** - High-level task groupings that the Lead Developer will decompose into detailed tasks

### Steps

1. **Initialize the Architect**
    - In your AI tool, create a new, clean chat thread named "Architect".
    - Set the agent's persona by using the contents of `.github/chatmodes/The Architect.chatmode.md` or copy the content for Cursor's custom modes.

2. **Start the Planning Session**
    - Reference to the `README.md` document and `DATA_CONTRACT.md` with @ or # in the chat context or just drag and drop them.
    - Ask the Architect to review the requirements and propose an initial system architecture.

3. **Collaborate on the Design**
    - Engage the Architect in a back-and-forth discussion about:
      - Tech stack choices for both UI prototype and CLI engine
      - System component boundaries and data flow
      - Folder structure and module organization
    - Challenge its suggestions, ask for alternatives, and guide it to final decisions.

4. **Generate Architecture Documentation**
    - Once the design is finalized, use the prompt from `.github/prompts/Architect Task Handover.prompt.md` or a similar reusable prompt.
    - The Architect will generate the four deliverable documents listed above. Note that you might need to reference the folder with @folder or #folder.
    - Review each document to ensure it provides clear guidance for implementation.

5. **Validate the Architecture**
    - Confirm the proposed architecture can deliver both the UI prototype and CLI engine within the workshop timeframe.
    - Ensure the data contract validation addresses any gaps or assumptions.


---

## Phase 2: Lead Developer (Implementation Planning)

**Goal:**  
Decompose the Architect's high-level plan into a detailed, actionable iteration backlog with well-defined sub-tasks.

### Expected Deliverables

- **`developer_todo.md`** - Specific, concise and accurate task breakdown with acceptance criteria for each sub-task
- **Handoff documents** - Clear instructions for the Implementer agent for each task group

### Steps

1. **Initialize the Lead Developer**
    - Create a new, clean chat thread named "Lead Developer".
    - Set the agent's persona using `.github/chatmodes/Lead Developer.chatmode.md`.

2. **Provide the Architecture Context**
    - Reference or paste all four documents from Phase 1:
      - `docs/system-architecture.md`
      - `docs/data-contract-validation.md` 
      - `docs/implementation-structure.md`
      - `TODO.md`
    - Tell the Lead Developer: "This is your mission. Review these architecture documents and prepare to create an implementation plan."

3. **Request Initial Assessment**
    - Ask the Lead Developer to:
      - Assess the architecture's feasibility
      - Identify any risks or dependencies
      - Propose an implementation sequence
    - Review the assessment and challenge any assumptions.

4. **Generate the Implementation Plan**
    - Ask the Lead Developer to create an initial plan, explaining:
      - Why tasks are sequenced in this order
      - What technical decisions it's making
      - How it's breaking down complex tasks
    - Challenge and refine the plan. Consider using another AI tool to validate the approach if unsure.

5. **Create Task Handoffs**
    - Use the prompt from `.github/prompts/Lead to Implementer.prompt.md`.
    - The Lead Developer will generate:
      - A `developer_todo.md` with numbered, concrete sub-tasks
      - Clear handoff instructions for each task group
    - Ensure tasks are small enough for GPT-4.1 to execute without ambiguity.

6. **Validate the Backlog**
    - Confirm each task has:
      - Clear acceptance criteria
      - Specific file references
      - No architectural decisions required
    - Tasks should be executable in isolation with minimal context.

---

## Phase 3: Implementer (Code Execution)

**Goal:**  
Write clean, working code for one specific task at a time, following the structured handoff documents from the Lead Developer.

### Expected Deliverables

- **Working code** for each assigned task with proper error handling
- **Task completion reports** or escalation reports when scope conflicts arise

### Implementation Approach

**Control Level:** You can choose how much control to maintain over the implementation:
- **Full Agent Control:** Let the Implementer execute the entire task autonomously (good for straightforward tasks)
- **Guided Implementation:** Stay engaged and review each step before proceeding (recommended for complex tasks)
- **Hybrid Approach:** Start autonomous, intervene when needed

**Structured Execution:** Even when letting the agent work independently, maintain structure. Don't try to implement everything at once—work step-by-step through the defined tasks.

### Steps

1. **Start a New Task Thread**
    - For each task listed in `developer_todo.md`, create a new, clean chat thread named "Implementer - Task [X]".
    - Every task must get its own isolated thread to prevent context mixing.

2. **Initialize the Implementer**
    - Set the agent's persona using `.github/chatmodes/Implementer.chatmode.md`.
    - Provide the specific task handoff document created by the Lead Developer using `.github/prompts/Lead to Implementer.prompt.md`.

3. **Execute the Task with Scope Awareness**
    - Give the agent the task-specific instructions from the handoff document.
    - **Critical Rule:** If the Implementer encounters unexpected issues or scope conflicts, it should STOP and ask:
      - "Does solving this exceed my original mandate?"
      - "Do I need Lead Developer input to decide which way to go?"
      - "Does the plan need to be updated or clarified?"
    - If yes to any of these, use `.github/prompts/Implementer Report.prompt.md` to generate a report back to the Lead Developer.

4. **Handle Scope Conflicts**
    - When the Implementer reports scope conflicts:
      - Return to the Lead Developer thread
      - Provide the Implementer's report
      - Get clarification or plan updates
      - Return to the Implementer with new instructions

5. **Complete and Validate**
    - Once the task is completed, validate it meets the acceptance criteria
    - Update the `developer_todo.md` to mark the task as complete

6. **Repeat**
    - Move to the next task in `developer_todo.md`, creating a new isolated thread
    - Continue until the backlog is complete

### Best Practices

- **Stay in Scope:** Don't let the Implementer solve problems outside its mandate
- **Escalate Early:** When in doubt, escalate to the Lead Developer rather than making architectural decisions
- **One Task, One Thread:** Never mix multiple tasks in the same conversation thread
- **Document Decisions:** Keep track of scope changes and decisions for future reference

### Alternative Approaches

**Note:** This structured, hierarchical approach is one model for managing AI-assisted development. In reality, you might want to:
- Use different working models for different types of tasks
- Occasionally take "exploration threads" to investigate unknowns before formal planning
- Adjust the level of structure based on your comfort with the codebase and requirements

The key is to choose your approach deliberately rather than jumping around without structure.
