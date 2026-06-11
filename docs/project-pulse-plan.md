# Project Pulse dashboard implementation plan

## Summary

Build **Project Pulse** as a small static dashboard in `app/` that presents project health in a polished, contributor-friendly card layout. The implementation should stay aligned with the existing exercise structure: plain static files, deterministic naming, and a VS Code launch configuration that serves from `app/` and opens `index.html` instead of a directory listing.

Current repo observations that shape this plan:

- `app/` exists but the target dashboard files are not present yet.
- `.vscode/tasks.json` already exists; `.vscode/launch.json` is not present yet.
- The project brief requires `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
- Step validation is phrase-based plus JSON parsing, so the implementation must include deterministic file names, selectors, and visible terminology.

---

## Ordered implementation steps

### Phase 1 — Confirm scope, data contract, and ownership
**Goal:** Lock the implementation shape before parallel work begins.

**Tasks**
1. Review the Project Pulse brief and step expectations.
2. Define the dashboard content contract:
   - top-level `projects` array in `app/project-data.json`
   - each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`
3. Confirm file ownership boundaries to avoid Designer/Coder conflicts.
4. Decide the rendering approach for `app/index.html`:
   - static HTML shell
   - references `styles.css`
   - references `project-data.json`
   - renders visible `project-card` entries from data

**File assignments**
- Planning only; no implementation file changes in this phase.
- Scope definition must explicitly cover:
  - `app/index.html`
  - `app/styles.css`
  - `app/project-data.json`
  - `.vscode/launch.json`

**Primary owner**
- Orchestrator / Planner

---

### Phase 2 — Define UI/UX and content structure
**Goal:** Produce a clear dashboard structure and visual direction before final implementation is assembled.

**Tasks**
1. Define the page hierarchy for Project Pulse:
   - page title
   - dashboard container
   - project card grid/list
   - per-card metadata layout
2. Define visual treatment for:
   - status badges
   - priority emphasis
   - readable spacing
   - responsive behavior
   - accessible contrast and typography
3. Specify CSS hooks that must exist:
   - `.dashboard`
   - `.project-card`
4. Specify how fields appear in the UI so Coder can wire rendering consistently.

**File assignments**
- `app/index.html` — Designer provides structural guidance only
- `app/styles.css` — Designer owns visual system, layout rules, responsive behavior, and polish

**Primary owner**
- Designer

**Designer responsibilities**
- Define information hierarchy for project cards
- Ensure the first view clearly reads as a dashboard, not a plain document
- Specify accessible spacing, contrast, and semantic layout expectations
- Ensure the design supports multiple projects and small-screen wrapping
- Recommend deterministic class names and badge treatments that match step validation

---

### Phase 3 — Create project data source
**Goal:** Establish the data file that drives visible dashboard content.

**Tasks**
1. Create `app/project-data.json` with a top-level `projects` key.
2. Add multiple realistic project objects.
3. Ensure every object includes:
   - `name`
   - `owner`
   - `status`
   - `recentActivity`
   - `priority`
4. Keep values concise and contributor-friendly.

**File assignments**
- `app/project-data.json` — Coder owns schema implementation and sample content

**Primary owner**
- Coder

**Coder responsibilities in this phase**
- Produce valid JSON only
- Keep the structure deterministic and easy to consume
- Include enough projects to make the dashboard visually meaningful
- Avoid schema drift beyond the required keys unless clearly justified

---

### Phase 4 — Build dashboard shell and data rendering
**Goal:** Implement the actual Project Pulse page and connect it to the JSON data.

**Tasks**
1. Create `app/index.html` with the exact title `Project Pulse`.
2. Reference `styles.css`.
3. Reference `project-data.json`.
4. Render visible project cards from the JSON data.
5. Use the class name `project-card` on each project card.
6. Make sure the UI visibly exposes:
   - status
   - recentActivity
   - priority
   - owner
   - name
7. Keep markup semantic and accessible.

**File assignments**
- `app/index.html` — Coder owns implementation; Designer input from Phase 2 must be applied

**Primary owner**
- Coder

**Dependencies**
- Depends on Phase 2 design direction
- Depends on Phase 3 data shape being settled

---

### Phase 5 — Implement polished dashboard styling
**Goal:** Make the dashboard visually complete and aligned with the exercise brief.

**Tasks**
1. Create `app/styles.css`.
2. Add a `.dashboard` selector for the main dashboard container.
3. Add a `.project-card` selector for project card styling.
4. Include polished UI treatments such as:
   - `border-radius`
   - `box-shadow`
   - spacing
   - responsive layout
   - badge styling
5. Ensure the styling supports the markup structure used in `app/index.html`.

**File assignments**
- `app/styles.css` — Designer defines the styling direction; Coder applies and finalizes implementation if the Orchestrator splits work that way

**Primary owner**
- Designer for design decisions
- Coder for final CSS implementation if only one agent writes code

**Dependencies**
- Depends on Phase 2
- Should stay coordinated with Phase 4 markup choices

---

### Phase 6 — Add runnable VS Code launch support
**Goal:** Make the dashboard easy to preview from Run and Debug.

**Tasks**
1. Create `.vscode/launch.json` as strict JSON with no comments.
2. Add a configuration named `Run Project Pulse Dashboard`.
3. Configure it to serve from the `app` directory.
4. Use `python3 -m http.server 5500`.
5. Ensure the launch opens `http://localhost:%s/index.html`.
6. Ensure the learner lands on the dashboard frontend, not a directory listing.

**File assignments**
- `.vscode/launch.json` — Coder owns

**Primary owner**
- Coder

**Dependencies**
- Can start once the app location and URL target are known
- Does not need completed CSS, but should be finalized after `app/index.html` path assumptions are stable

---

### Phase 7 — Integration review and validation
**Goal:** Verify the dashboard matches both the brief and repo validation patterns.

**Tasks**
1. Verify file existence:
   - `app/index.html`
   - `app/styles.css`
   - `app/project-data.json`
   - `.vscode/launch.json`
2. Verify content expectations:
   - `Project Pulse` appears in `app/index.html`
   - `styles.css` is referenced
   - `project-data.json` is referenced
   - `project-card` appears in markup
   - `.dashboard` and `.project-card` appear in CSS
   - `border-radius` and `box-shadow` appear in CSS
   - JSON includes `projects`, `name`, `owner`, `status`, `recentActivity`, `priority`
3. Parse-check JSON files.
4. Run the VS Code launch configuration and confirm it opens `index.html`.

**File assignments**
- Validation across:
  - `app/index.html`
  - `app/styles.css`
  - `app/project-data.json`
  - `.vscode/launch.json`

**Primary owner**
- Coder validates implementation
- Designer reviews visual/accessibility quality
- Orchestrator confirms handoff completeness

---

## Dependencies between steps

1. **Phase 1 must happen first**  
   It fixes scope, file ownership, and the data contract.

2. **Phase 2 should happen before final HTML/CSS implementation**  
   It reduces churn by defining layout and styling direction early.

3. **Phase 3 must happen before final data-driven rendering in Phase 4**  
   `app/index.html` needs a stable JSON shape.

4. **Phase 4 and Phase 5 are tightly coupled**  
   Markup and styling should be coordinated; minor iteration between them is expected.

5. **Phase 6 depends on stable file paths and launch assumptions**  
   It should not be finalized until `app/index.html` is confirmed as the app entry point.

6. **Phase 7 is last**  
   Validation depends on all implementation files existing.

---

## Work that can run in parallel

### Safe parallel work
1. **Phase 2 (Designer UI direction)** and **Phase 3 (Coder data file)**  
   **Why:** The JSON schema is already defined by the brief, so sample data creation can proceed while design decisions are being made.

2. **Early draft of Phase 6 (`.vscode/launch.json`)** can begin during Phase 4  
   **Why:** The server command, port, app directory, and target file are mostly predetermined by the exercise.

3. **Designer review of markup semantics** can happen while Coder refines CSS/launch config  
   **Why:** Review does not require file ownership overlap if feedback is routed through the Orchestrator.

### Parallel work with caution
1. **Phase 4 (`app/index.html`)** and **Phase 5 (`app/styles.css`)**  
   **Why caution:** They can proceed in parallel only if the Orchestrator locks class names and structure first. Otherwise, repeated CSS/markup churn is likely.

---

## Work that must run sequentially

1. **Scope confirmation before implementation**  
   Avoids conflicting assumptions about rendering, selectors, and launch behavior.

2. **Data contract before final HTML data rendering**  
   The page should not implement against an unstable schema.

3. **Final launch config after entry page is confirmed**  
   Prevents a configuration that opens the wrong route or directory listing.

4. **Validation after all files are in place**  
   Repo checks depend on final file content and JSON validity.

---

## Edge cases to handle

1. **Directory listing instead of dashboard UI**  
   The launch configuration must open `index.html`, not just the server root.

2. **JSON parses but does not match expected keys**  
   Every project object must include all required fields.

3. **HTML references the data file but does not visibly render cards**  
   The implementation should show actual project cards, not just include a placeholder.

4. **CSS looks polished on desktop only**  
   The layout should remain readable on narrower widths.

5. **Class/selector mismatch between HTML and CSS**  
   `project-card` in HTML must align with `.project-card` in CSS.

6. **Designer/Coder ownership collisions**  
   Without explicit boundaries, both agents could change `app/index.html` or `app/styles.css` in incompatible ways.

7. **Static-file fetch/path issues**  
   The implementation should assume the app is served from `app/`, so relative paths must work from that location.

8. **Validation phrase misses**  
   Even a working dashboard can fail the exercise if deterministic phrases/selectors are absent.

---

## Validation expectations

Validation should cover both **exercise-specific checks** and **functional behavior**.

### Repository-aligned validation
- `docs/project-pulse-plan.md` includes:
  - `Project Pulse`
  - `Designer`
  - `Coder`
  - `app/index.html`
  - `app/styles.css`
  - `app/project-data.json`
  - `.vscode/launch.json`
  - `dependencies`
  - `parallel`
  - `validation`

### Implementation validation
- `app/project-data.json` parses as valid JSON
- `.vscode/launch.json` parses as valid JSON
- `app/index.html` includes `Project Pulse`
- `app/index.html` references `styles.css`
- `app/index.html` references `project-data.json`
- `app/index.html` includes visible `project-card` usage
- `app/index.html` exposes `status`, `recentActivity`, and `priority`
- `app/styles.css` includes `.dashboard`
- `app/styles.css` includes `.project-card`
- `app/styles.css` includes `border-radius`
- `app/styles.css` includes `box-shadow`
- `app/project-data.json` includes:
  - `projects`
  - `name`
  - `owner`
  - `status`
  - `recentActivity`
  - `priority`
- `.vscode/launch.json` includes `Run Project Pulse Dashboard`
- `.vscode/launch.json` is configured to open `index.html`

### Functional validation
- Run the VS Code launch configuration
- Confirm the browser opens the Project Pulse dashboard
- Confirm the opened URL resolves to `index.html`
- Confirm multiple project cards are visible
- Confirm the page is usable at smaller viewport widths
- Confirm the UI is readable without overlapping or clipped content

---

## File assignments by workstream

### Designer-owned or Designer-led
- `app/styles.css`
  - visual system
  - spacing
  - responsive layout
  - card styling
  - badge treatment
  - accessibility-oriented styling decisions
- `app/index.html` (advisory responsibility)
  - content hierarchy
  - semantic structure recommendations
  - card information order

### Coder-owned
- `app/project-data.json`
  - final schema-compliant project data
- `app/index.html`
  - page implementation
  - data reference
  - rendering logic
  - semantic markup
- `.vscode/launch.json`
  - runnable preview configuration
- `app/styles.css`
  - final implementation of approved design decisions if the Orchestrator has Coder apply Designer guidance

### Orchestrator coordination expectation
- Keep `app/index.html` ownership single-threaded at merge time
- Keep `app/styles.css` ownership single-threaded at merge time
- Route design feedback through the Orchestrator before Coder finalizes

---

## Open questions

1. Should the dashboard include only the required fields, or also the “short contributor-friendly summary” mentioned in the brief?
2. Should `priority` be presented as risk language, urgency language, or a neutral priority badge?
3. Should the project cards be rendered entirely client-side from JSON, or is a simpler static fallback acceptable if the JSON is still referenced?
4. How many sample projects are ideal for the initial dataset: minimum three for visual credibility, or more?
5. Should status values be normalized to a fixed set such as `On Track`, `At Risk`, and `Blocked` to simplify badge styling?

## Concise summary

Structure: 7 phases from scope definition through validation, with explicit file ownership for `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`, plus Designer/Coder responsibilities, dependencies, parallel/sequential decisions, edge cases, and validation expectations.

Notable assumptions:
- `docs/` already exists, so no new docs directory is needed.
- The dashboard is a plain static app in `app/`.
- The launch config should use `python3 -m http.server 5500`, serve from `app/`, and open `index.html`.
- Validation should align with the existing workflow checks already present in the repo.

Requirements:
- Save to `docs/project-pulse-plan.md`.
- Create `docs/` if it does not exist.
- Do not stage, commit, or push changes.
- Return a brief confirmation including whether the file was written successfully.
