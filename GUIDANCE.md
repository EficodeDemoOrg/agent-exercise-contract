# Workshop Guidance: Process-Driven AI Development

## Objective
Build the "Digital Grade Checker" MVP from scratch using a structured, artifact-driven workflow that leverages AI assistance effectively. This guide shifts focus from agent personas to clear processes and deliverables.

## Core Principles

### Manage Your Context
Your context window is a resource. Aim to keep your input (prompts + files) below 40-60% of the total limit. This leaves the AI enough room to think and generate a complete response.

### Separate Reading from Writing
Phases 1 (Research) and 2 (Planning) are for understanding; you should be reading and analyzing files. Phase 3 (Execution) is for generating; you should be focused on writing code for small, well-defined tasks.

### One Thread, One Goal
Use separate conversation threads for research, planning, and each individual implementation task. This prevents context bleed and keeps the AI focused.

## Why This Approach?

This workflow builds habits for effective AI collaboration by reinforcing good human practices: breaking problems into manageable pieces, maintaining focus, and taking strategic pauses instead of frantically forcing solutions.

**Context Management:** AI tools have limited context. This prevents "overflow" by having each phase focus on specific artifacts and outcomes.

**Artifact-Driven Development:** Each phase produces concrete deliverables that become the foundation for the next phase, creating a clear progression from understanding to implementation.

**Thread Isolation:** One conversation per domain/task. Use **Thread Dump** prompt (`.github/prompts/Thread Dump.prompt.md`) to transfer context when needed.

This prevents common pitfalls: jumping between tasks, mixing contexts, and losing track of what the AI is doing. The key principle is **deliberate context isolation** that supports both human understanding and AI effectiveness.

---

**Tooling Note:** Templates and prompts are available in the repository. The way you use them differs between tools.

**Agent Templates:** For Copilot, these are defined in `.github/chatmodes`. Cursor's "Custom Modes" are configured within the tool and are not directly visible in the project files. For Cursor it is possible to copy the content of these files and include the instructions into the custom mode.

**Reusable Prompts:** Copilot uses `.github/prompts`. For Cursor, you can create a local `.cursor/prompts` folder and @-reference the files.

## Phase 1: Research & Discovery (Interactive Research)

**Goal:**  
Collaboratively explore the project requirements with the AI to produce a comprehensive summary of the problem space.

**Objective:** This phase replaces traditional architecture roles. Its sole purpose is to deeply understand the problem, not to finalize the architecture.

### Expected Deliverable

- **`research.md`** - A comprehensive understanding document containing:
  - Summary of project goals
  - List of known constraints and requirements
  - Initial thoughts on potential tech stack choices (as ideas, not final decisions)
  - List of open questions or assumptions that need validation

### Steps

1. **Initialize Interactive Research Session**
    - Create a new, clean chat thread named "Research & Discovery".
    - Use a templated, interactive prompt that guides the AI to ask clarifying questions about requirements, constraints, user stories, and technical context before proposing solutions.

2. **Engage in Collaborative Dialogue**
    - Reference the `README.md` and `DATA_CONTRACT.md` with @ or # in the chat context or drag and drop them.
    - Let the AI consume these documents and ask clarifying questions.
    - This is a **read-heavy phase** - focus on understanding, not implementing.

3. **Explore Requirements Together**
    - Engage in back-and-forth discussion about:
      - Project requirements and constraints
      - User stories and success criteria
      - Technical context and existing systems
      - Potential approaches and trade-offs
    - The AI should be asking YOU questions to understand the problem space.

4. **Validate Understanding**
    - Ensure the AI has a comprehensive understanding of:
      - What success looks like
      - What constraints exist
      - What assumptions need to be validated
      - What technical options are available

5. **Generate Research Summary**
    - Once understanding is complete, ask the AI to generate the `research.md` document.
    - Review to ensure it captures the full problem space without premature solution commitments.

---

## Phase 2: Implementation Planning

**Goal:**  
Take the validated research.md and turn it into an actionable engineering plan with concrete steps and technical decisions.

### Expected Deliverable

- **`plan.md`** - A detailed, step-by-step implementation plan structured with:
  - Clear implementation phases
  - Technical steps with specific file/code references
  - Success criteria for each phase
  - Testing and validation approaches

### Steps

1. **Initialize Implementation Planning**
    - **Start a new thread** named "Implementation Planning".
    - Provide the `research.md` as the core context.
    - This remains a **read-heavy phase** as the AI synthesizes research into a structured plan.

2. **Guide Plan Creation**
    - Ask the AI to create a detailed implementation plan based on the research findings.
    - The AI should outline:
      - Implementation phases in logical order
      - Specific technical changes required
      - File structures and code organization
      - Testing and validation criteria

3. **Refine and Validate Plan**
    - Review the plan for completeness and feasibility.
    - Challenge assumptions and ask for alternatives where needed.
    - Ensure the plan is concrete enough to guide implementation.

4. **Finalize Implementation Strategy**
    - Confirm the plan addresses all requirements from the research phase.
    - Ensure success criteria are clear and measurable.
    - Validate that the plan can be broken down into discrete tasks.

---

## Phase 3: Task Execution (Two-Step Process)

### Step 3a: Task Decomposition

**Goal:**  
Break down the high-level plan.md into small, executable tasks.

**Objective:** Transform the implementation plan into granular, self-contained tasks that can be executed in isolation.

#### Expected Deliverable

- **`developer_todo.md`** - A list of small, concrete implementation tasks where each item:
  - Is self-contained and executable in isolation
  - Includes specific instructions for implementation
  - Has clear acceptance criteria
  - Requires minimal additional context

#### Steps

1. **Initialize Task Decomposition**
    - **Start a new thread** named "Task Decomposition".
    - Provide the `plan.md` as context.

2. **Generate Task Breakdown**
    - Ask the AI: "Based on this plan, generate a list of small, concrete implementation tasks. Each task should be executable in isolation and include specific instructions for the implementer."
    - Ensure tasks are granular enough for focused implementation.

3. **Validate Task Quality**
    - Review each task to ensure it:
      - Can be completed independently
      - Has clear, specific instructions
      - Includes acceptance criteria
      - Doesn't require architectural decisions

### Step 3b: Task Execution

**Goal:**  
Write code for one task at a time using isolated, focused conversations.

**Objective:** This is the primary **write-heavy phase** where actual code gets generated.

#### Expected Deliverables

- **Working code** for each assigned task with proper error handling
- **Task completion confirmation** or escalation reports when scope conflicts arise

#### Steps

1. **Execute Tasks One by One**
    - For each item in `developer_todo.md`, **start a new, isolated thread** named "Task [X] - [Brief Description]".
    - Provide only the specific instructions for that single task.
    - The AI should focus solely on writing code for that specific task.

2. **Maintain Task Isolation**
    - **Critical Rule:** Each task gets its own conversation thread.
    - Provide minimal context - just the task instructions and any directly relevant files.
    - Keep the AI focused on the specific implementation requirements.

3. **Handle Scope Issues**
    - If the task reveals larger issues or scope conflicts:
      - Stop implementation
      - Document the issue
      - Return to the Task Decomposition thread to revise the plan
      - Create new, refined tasks as needed

4. **Complete and Validate**
    - Once each task is completed, validate it meets the acceptance criteria.
    - Update `developer_todo.md` to mark tasks as complete.
    - Move to the next task with a fresh thread.

### Best Practices for Task Execution

- **Stay Focused:** Each thread should accomplish exactly one task
- **Escalate When Needed:** If scope exceeds the task definition, stop and revise the plan
- **Document Progress:** Keep `developer_todo.md` updated with completion status
- **Maintain Isolation:** Resist the urge to handle multiple tasks in one conversation

### Alternative Approaches

**Note:** This structured approach provides a framework for managing AI-assisted development. You can adapt it based on:
- Task complexity and your comfort level
- Time constraints and project scope
- Your preferred level of AI autonomy vs. human guidance

The key is to choose your approach deliberately rather than jumping around without structure.
