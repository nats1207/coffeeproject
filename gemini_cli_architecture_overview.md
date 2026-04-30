# Gemini CLI: Agents, Skills, and Tools Overview

This document summarizes the architecture and relationship between the Main Agent, Subagents, Skills, and Tools within the Gemini CLI ecosystem.

## 1. The Main Agent vs. Subagents

| Feature | Main Agent (Orchestrator) | Subagent (Specialist) |
| :--- | :--- | :--- |
| **Role** | Project Manager & Strategy. | Task execution & deep research. |
| **Lifespan** | Persistent (entire session). | Ephemeral (task-specific). |
| **Context** | Full conversation history. | Isolated "Clean Slate" loop. |
| **Efficiency** | Conserves tokens for long-term memory. | Can "burn" context for complex tasks. |
| **Analogy** | The Architect. | The Specialized Contractor. |

### The "Signal vs. Noise" Effect
When a subagent completes a task, it returns a concise summary to the Main Agent. All the messy, turn-heavy internal logic (reading dozens of files, trial-and-error commands) is discarded, keeping the Main Agent's history clean and fast.

## 2. Skills: The Procedural Framework
Skills are modular packages that provide "how-to" knowledge and resources.

*   **SKILL.md:** Detailed instructions and workflows.
*   **Scripts:** Executable code for deterministic tasks.
*   **References:** Documentation and schemas.
*   **Assets:** Templates, icons, or boilerplate code.

**Key Rule:** Subagents **can** activate skills, but they **cannot** call other subagents (recursion protection).

## 3. Tools and Permissions
A subagent's abilities are defined in the **YAML frontmatter** of its `.md` definition file.

*   **Native Tools:** Abilities like `read_file`, `grep_search`, or `run_shell_command`.
*   **Permissions:** Use the `tools` list to "sandbox" an agent (e.g., an agent with only `read_file` is read-only).
*   **The "Hands vs. Toolkit" Analogy:**
    *   **Tools** are the agent's "hands" (the ability to act).
    *   **Skills** are the "toolbox" (the specialized equipment).
    *   An agent needs the `run_shell_command` tool to actually use a script found inside a skill.

## 4. Customizing the Toolkit

### Model Context Protocol (MCP)
The "Professional" way to add new native tools. It allows you to connect the agent to external databases, APIs, or local services via a standardized server protocol.

### Skill Scripts
The "Quick" way to add tools. You write a script, put it in a skill, and instruct the agent to run it via `run_shell_command`.

## 5. Summary of Interactions
*   **Main Agent** → Invokes → **Subagent** (Isolation)
*   **Subagent** → Activates → **Skill** (Expertise)
*   **Skill** → Contains → **Scripts** (Custom Actions)
*   **Subagent** → Uses → **Tools** (Native Abilities)
