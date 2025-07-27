# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains prompt templates for structured web application development workflows using Claude Code's specialized agents. The templates guide the development process through a series of steps, each handled by a specific agent.

## Commands

### Custom Git Commands
Located in `.claude/commands/`:
- `/git-init [repo-url]` - Initialize new GitHub repository
- `/git-commit-push [message]` - Commit and push changes
- `/git-undo [what]` - Undo changes (local or remote)
- `/git-reset` - Reset to latest GitHub version (⚠️ deletes all local changes)

### Agent Invocation
Use the `Task` tool with the appropriate `subagent_type` parameter to invoke each agent:
```python
Task(description="Step 1: Validate idea", prompt="[user's idea description]", subagent_type="idea-validator")
```

## Development Workflows

### 1. New Application Development

When creating a new application from scratch, follow this strict sequence:
1.  `step1_idea-validator` - Validate and research the idea
2.  `step2_requirements-analyst` - Create detailed technical requirements
3.  `step3_frontend-architect` - Design the frontend architecture
4.  `step4_ui-architect` - Establish the design system
5.  `step5_layout-designer` - Create responsive layouts
6.  `step6_component-builder` - Build UI components
7.  `step7_api-integrator` - Integrate with backend APIs
8.  `step8_performance-optimizer` - Optimize application performance
9.  `step9_accessibility-tester` - Ensure WCAG compliance

### 2. Website Redesign

For redesigning existing websites, follow this modified sequence:
1.  `site-redesign-analyst` - Audit the existing site
2.  `idea-validator` - Create a redesign plan (not new ideas)
3.  `requirements-analyst` - Document requirements, preserving all functionality
4.  `ui-architect` - Create a modern design system compatible with existing tech
5.  `component-builder` - Wrap existing components with new styles
6.  Skip `api-integrator` - APIs remain unchanged
7.  `performance-optimizer` - Optimize frontend assets only
8.  `accessibility-tester` - Improve accessibility with new styles

## Important Workflow Rules (Agent Workflow)

1.  **Stop After Each Agent**: After each agent completes its work, stop and report:
    * Which step was completed.
    * What documents were created in `docs/`.
    * Ask the user to review the result before continuing.
    * Wait for explicit confirmation ("да", "продолжаем", "дальше", "ok", "proceed", "next") to move to the next step.

2.  **Documentation Structure**: Each agent creates documentation in its own subdirectory:
    * `docs/step1_idea-validator/`
    * `docs/step2_requirements-analyst/`
    * etc.

3.  **Progressive Enhancement (for Redesigns)**: The priorities for a redesign are:
    * Preserve **100% of existing functionality**.
    * Only update visual and UX elements.
    * Maintain compatibility with the existing tech stack.
    * Carefully wrap components without breaking their functionality.

## General Development Principles & Coding Standards

This section complements the agent-specific rules and establishes general standards for writing code.

### Core Principles

* **Simplicity and Clarity**: Always prefer simple and clear solutions.
* **Minimize Code**: Reduce the number of lines of code without sacrificing readability.
* **Don't Repeat Yourself (DRY)**: Before implementing a new feature, check the codebase for similar functionality.
* **Implementation Plan**: Create a step-by-step plan of action before making changes.
* **Clean Codebase**: Keep the code clean and organized. Avoid temporary scripts in permanent files.
* **File Size**: Limit file sizes to 200-300 lines. Refactor when this limit is exceeded.
* **Change History**: All significant changes must be documented in `history.md`.

### Coding Conventions

* **Code Language**: All code (variables, functions, classes, methods) must be written **exclusively in English**. Avoid transliteration.
* **Syntax**: Logical operators (`if`, `else`, `while`, `for`) and library calls must strictly follow their original English syntax.
* **Comments**: Comments in the code **can be written in Russian**. Do not delete existing comments.
* **UI Constants**: Text constants for the user interface can be in any language as per requirements.
* **Linters**: Always use linters to maintain code quality.

### Coding Workflow

* **Task Focus**: Concentrate exclusively on the code sections directly related to the current task. Do not alter code unrelated to the task.
* **Testing**: Always write detailed tests for key functionalities.
* **Architectural Changes**: Do not make significant changes to the architecture or design patterns without explicit instruction.
* **Impact Assessment**: Before each change, assess its potential impact on other parts of the code.
* **Completion**: Fully complete the current task before moving on to the next one.

### Environment and Security

* **Environments**: Be mindful of the differences between **dev, test, and prod** environments.
* **Mock Data**: Mock data should **only be used for tests** and must never be present in dev or prod environments.
* **`.env` File**: Never overwrite the `.env` file without prior agreement and confirmation.

## Project Structure

* **Prompt Templates**: Located in the root directory as `.txt` files.
    * `ВАЖНО используй - Шаблон промпта для создания с нуля.txt` - Template for new application development.
    * `ВАЖНО используй - Шаблон промпта для редизайна вашего приложения.txt` - Template for website redesign.
* **Custom Commands**: Located in `.claude/commands/` as `.md` files.
* **Documentation**: Generated by agents in `docs/` subdirectories during the workflow execution.

## Technical Stack

* **Backend**: Python
* **Frontend**: HTML5/CSS/JS/REACT

## Key Operating Principles

* Each agent builds upon the work of the previous agents.
* User control and review at each step is mandatory.
* Documentation is created progressively in the `docs/` folder.
* During a redesign, existing functionality **must never be compromised**.
