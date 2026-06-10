# Agent team

Mona's Project Pulse dashboard uses a four-agent custom team orchestrated from **GitHub Copilot CLI in a Codespace**. The CLI acts as the control point for delegating planning, implementation, and design work across the repository-defined agents in `.github/agents/`.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates the full delivery flow, gets a plan from Planner, assigns scoped work to Coder and Designer, sequences or parallelizes phases, and checks that the integrated result hangs together. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Researches the repo and relevant docs, identifies dependencies and edge cases, and produces the implementation plan and phase breakdown for the dashboard work. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements the dashboard code, fixes bugs, keeps behavior explicit and testable, and can add runnable app support such as `.vscode/launch.json` for Project Pulse when assigned. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Shapes the dashboard UX and visual system, including layout, accessibility, responsive behavior, project cards, badges, spacing, and overall frontend polish. | `.github/agents/designer.agent.md` |

In practice, the **Orchestrator** uses **Planner** to turn Mona's dashboard request into phases, then delegates implementation to **Coder** and UI/UX refinement to **Designer** with explicit file scopes so the work stays coordinated.
