# Agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate Mona's Project Pulse dashboard team.

## Orchestrator

- **Target model:** Claude Opus 5.5 (copilot)
- **Responsibility:** Coordinates the Planner, Coder, and Designer; turns the implementation plan into phased work, delegates non-overlapping file scopes, resolves dependencies, and verifies that the integrated dashboard is coherent.
- **Definition:** [.github/agents/orchestrator.agent.md](../.github/agents/orchestrator.agent.md)

## Planner

- **Target model:** Claude Opus 5.5 (copilot)
- **Responsibility:** Researches the repository and requirements, identifies implementation steps and edge cases, maps file assignments and dependencies, and produces a practical plan for the team.
- **Definition:** [.github/agents/planner.agent.md](../.github/agents/planner.agent.md)

## Coder

- **Target model:** GPT-5.5 (copilot)
- **Responsibility:** Implements the dashboard code and support configuration with clear structure, deterministic behavior, explicit errors, and testable results.
- **Definition:** [.github/agents/coder.agent.md](../.github/agents/coder.agent.md)

## Designer

- **Target model:** Gemini 3.7 Flash (copilot)
- **Responsibility:** Designs the UI/UX, accessibility, information hierarchy, responsive layout, visual treatment, and dashboard-specific Project Pulse styling.
- **Definition:** [.github/agents/designer.agent.md](../.github/agents/designer.agent.md)
