# Workshop Guidance: Process-Driven AI Development

## Objective
Build your chosen MVP project from scratch using a structured, artifact-driven workflow that leverages AI assistance effectively. This guide shifts focus from agent personas to clear processes and deliverables.

Choose between:
- **Digital Grade Checker**: Construction technology tool with frontend/backend paths
- **Context Window Visualizer**: AI debugging tool with integrated web application

## Core Principles

### Manage Your Context
Your context window is a resource. Aim to keep your input (prompts + files) below 40-60% of the total limit. This leaves the AI enough room to think and generate a complete response.

### Separate Reading from Writing
Phases 1 (Research) and 2 (Task Execution) are for understanding; you should be reading and analyzing files. Phase 2 (Execution) is for generating; you should be focused on writing code for small, well-defined tasks.

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

## Phase 0: Blueprint Creation (Foundational Architecture)

**Goal:**  
Collaborate with an AI Architect to establish foundational technical decisions for a new, greenfield project.

**Objective:** Create the high-level technical blueprint that captures core architectural decisions before diving into detailed research and implementation.

### When to Use This Phase
- Starting a completely new project from specifications
- Need to establish technology stack, architectural patterns, and high-level components
- Want to capture fundamental decisions that will guide all subsequent development

### Expected Deliverable
- **`BLUEPRINT.md`** - A foundational document containing:
  - Technology stack decisions (frontend, backend, database, deployment)
  - Architectural pattern choice (monolithic, microservices, serverless)
  - High-level component breakdown
  - Initial data model structure
  - Authentication strategy
  - Human validation sections for each major decision

### Steps

1. **Initialize Blueprint Session**
    - Create a new, clean chat thread named "Blueprint Creation".
    - Use the `Create Blueprint.prompt.md` template from `.github/prompts`.
    - Provide project specifications or requirements documents.

2. **Collaborative Architecture Discussion**
    - Engage with the AI Architect to explore technology choices
    - Discuss pros and cons of different architectural approaches
    - Make foundational decisions about stack, patterns, and structure
    - Ensure all major decisions are captured with reasoning

3. **Generate and Validate Blueprint**
    - AI creates the structured `BLUEPRINT.md` document
    - Review each section carefully and provide validation comments
    - Iterate on any decisions that need refinement
    - Ensure the blueprint provides clear guidance for subsequent phases

4. **Context Integration**
    - Add concise architectural summary to `.github/copilot-instructions.md`
    - Ensure core decisions are available for all future AI interactions

### Transition to Research Phase
Once the blueprint is validated, use it as foundational context for Phase 1 (Research & Discovery) to dive deeper into implementation details.

---

## Phase 1: Research & Discovery (Interactive Research)

**Goal:**  
Collaboratively explore the project requirements with the AI to produce a comprehensive summary of the problem space.

**Objective:** Building on the foundational blueprint from Phase 0, dive deeper into implementation requirements, constraints, and technical details needed for concrete planning.

### Expected Deliverable

- **`research.md`** - A comprehensive understanding document containing:
  - Summary of project goals and detailed requirements
  - List of known constraints and technical limitations
  - Implementation considerations based on the established architecture
  - List of open questions or assumptions that need validation before planning

### Steps

1. **Initialize Interactive Research Session**
    - Create a new, clean chat thread named "Research & Discovery".
    - Provide the validated `BLUEPRINT.md` as foundational context.
    - Use a templated, interactive prompt that guides the AI to ask clarifying questions about implementation requirements, constraints, and technical details.

2. **Engage in Collaborative Dialogue**
    - Reference your project's key documents with @ or # in the chat context or drag and drop them:
      - **For Digital Grade Checker**: `README.md`, `DATA_CONTRACT.md`, and validated `BLUEPRINT.md`
      - **For Context Window Visualizer**: `CONTEXT_WINDOW.md` and validated `BLUEPRINT.md`
    - Let the AI consume these documents and ask clarifying questions about implementation details.
    - This is a **read-heavy phase** - focus on understanding implementation requirements, not implementing.

3. **Explore Requirements Together**
    - Engage in back-and-forth discussion about:
      - Detailed implementation requirements within the established architecture
      - Technical constraints and integration challenges
      - User stories and acceptance criteria
      - Implementation approaches and trade-offs within the chosen stack
    - The AI should be asking YOU questions to understand implementation details and constraints.

4. **Validate Understanding**
    - Ensure the AI has a comprehensive understanding of:
      - How to implement the project within the established architectural framework
      - What specific constraints exist for implementation
      - What assumptions need validation before detailed planning begins
      - What technical details are needed for concrete implementation planning

5. **Generate Research Summary**
    - Once understanding is complete, ask the AI to generate the `research.md` document.
    - Review to ensure it captures implementation requirements and constraints without contradicting the established blueprint.

---

## Phase 2: Task Execution (Two-Step Process)

### Step 2a: Task Decomposition

**Goal:**  
Transform the validated research and blueprint into small, executable implementation tasks.

**Objective:** Bridge the gap between high-level architecture (blueprint) and detailed requirements (research) by creating granular, self-contained tasks that can be executed in isolation.

#### Expected Deliverable

- **`developer_todo.md`** - A list of small, concrete implementation tasks where each item:
  - Is self-contained and executable in isolation
  - Includes specific instructions for implementation
  - Has clear acceptance criteria
  - Requires minimal additional context

#### Steps

1. **Initialize Task Decomposition**
    - **Start a new thread** named "Task Decomposition".
    - Provide both the `BLUEPRINT.md` and `research.md` as context.
    - Use the `Create Plan.prompt.md` template from `.github/prompts` for structured task breakdown.

2. **Generate Task Breakdown**
    - Ask the AI: "Based on the blueprint architecture and research findings, generate a list of small, concrete implementation tasks. Each task should be executable in isolation and include specific instructions for the implementer."
    - Ensure tasks follow the architectural decisions from the blueprint
    - Ensure tasks address the requirements and constraints from research

3. **Validate Task Quality**
    - Review each task to ensure it:
      - Can be completed independently
      - Has clear, specific instructions
      - Includes acceptance criteria
      - Aligns with both blueprint and research findings
      - Doesn't require additional architectural decisions

### Step 2b: Task Execution

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
      - Return to the Task Decomposition thread to revise the task list
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
