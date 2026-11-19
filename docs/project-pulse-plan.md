# Project Pulse Implementation Plan

## Summary

Build Mona's lightweight, static Project Pulse dashboard for contributors. The result should present
multiple projects as readable cards, with project name, owner, status, recent activity, and priority
or risk clearly visible. The app will use three static files:

- `app/index.html` for semantic structure and project rendering
- `app/styles.css` for the polished dashboard presentation
- `app/project-data.json` for the project dataset

Create `.vscode/launch.json` so the VS Code **Run Project Pulse Dashboard** configuration runs
`python3 -m http.server 5500` with `cwd` set to `${workspaceFolder}/app`, then opens
`http://localhost:%s/index.html`. The launch file must be strict JSON with no comments.

The Orchestrator owns integration and sequencing. The Planner supplies this plan. The Designer owns
visual and accessibility decisions; the Coder owns the HTML, CSS, JSON, and launch implementation.

## Ordered implementation steps

1. **Establish the dashboard contract**
   - Coder and Designer confirm the visual structure and data fields before implementation.
   - Coder owns `app/project-data.json` and defines at least three varied, realistic projects.
   - The top-level key must be `projects`; every project must contain `name`, `owner`, `status`,
     `recentActivity`, and `priority`.

2. **Create the data and HTML structure in parallel**
   - Coder creates `app/project-data.json` with valid, deterministic JSON.
   - Coder creates `app/index.html` with the exact title `Project Pulse`, semantic page landmarks,
     links to `styles.css`, and a reference or load mechanism for `project-data.json`.
   - Coder assigns each rendered project the `project-card` class and renders `status`,
     `recentActivity`, and `priority`.
   - Designer reviews the proposed heading, card hierarchy, and status/priority treatment before
     final markup is integrated.

3. **Create the responsive visual design**
   - Designer assigns all experience decisions and provides the visual specification.
   - Coder implements it in `app/styles.css`, because the Coder owns implementation files.
   - The stylesheet must include `.dashboard` and `.project-card`, use `border-radius` and
     `box-shadow`, and provide a responsive layout that remains readable on small screens.
   - Use clear typography, contrast, status badges, visible priority/risk affordances, consistent
     spacing, focus states, and reduced-motion or semantic fallbacks where applicable.

4. **Integrate and implement the launch configuration**
   - Coder creates `.vscode/launch.json` after the app files are in place.
   - The file must use strict JSON syntax and contain no comments.
   - Name the launch configuration `Run Project Pulse Dashboard`.
   - Set `cwd` to `${workspaceFolder}/app`, run `python3 -m http.server 5500`, and configure
     `serverReadyAction` to open `http://localhost:%s/index.html`.
   - Designer should verify that the dashboard is the default browser target, not the app directory.

5. **Integrate and inspect**
   - Coder connects the data to the card rendering and verifies HTML/CSS references.
   - Orchestrator resolves integration conflicts and confirms the visual hierarchy matches the brief.
   - Stop only after the four implementation files are internally consistent.

6. **Validate and report**
   - Run the measurable checks listed below.
   - The Orchestrator records successful checks, any limitations, and the final handoff.
   - No git staging, committing, pushing, or other repository mutation is part of implementation
     planning or validation.

## File assignments

| File | Primary owner | Responsibility |
| --- | --- | --- |
| `app/index.html` | Coder | Project Pulse title, semantic structure, stylesheet/data references, project-card markup, and visible status, recent activity, and priority output |
| `app/styles.css` | Coder implementing; Designer guiding | `.dashboard` and `.project-card`, polished card treatment, status/priority visuals, readable spacing, responsive behavior, and accessible contrast |
| `app/project-data.json` | Coder | Valid top-level `projects` array and complete project records |
| `.vscode/launch.json` | Coder | Strict-JSON VS Code launch configuration using `app/` as `cwd` and opening `index.html` |

Designer should not edit JSON or launch configuration unless the Orchestrator explicitly expands the
scope. Coder should not change design direction by replacing the assigned visual/accessibility
decisions. The Orchestrator may review all files.

## Designer responsibilities

- Define information hierarchy, card layout, status and priority styling, spacing, typography, and
  responsive breakpoints.
- Create a clearly polished dashboard rather than a bare HTML page.
- Specify deterministic `.dashboard` and `.project-card` hooks.
- Ensure cards use `border-radius`, `box-shadow`, clear contrast, readable text, visible focus
  indicators, and useful status distinctions.
- Review desktop and narrow/mobile layouts and recommend empty, loading, or error presentation
  without changing Coder-owned files directly.
- Report design decisions and validation recommendations.

## Coder responsibilities

- Implement the HTML, CSS, JSON, and launch configuration within the assigned files.
- Keep the static app dependency-free and use clear, predictable JavaScript if rendering from JSON.
- Make fetch/render behavior deterministic and fail visibly if project data cannot be parsed.
- Create the strict-JSON `.vscode/launch.json` with the requested name and target.
- Run syntax and file checks, preview the app, and report remaining risks.
- Do not stage, commit, or push changes.

## Dependencies

- `app/index.html` depends on the field names and shape in `app/project-data.json`.
- `app/styles.css` depends on the markup and `project-card` hook in `app/index.html`.
- `.vscode/launch.json` depends on `app/index.html` existing and on Python 3 serving the app directory.
- The final launch preview depends on all three app files being present.
- Final validation depends on successful JSON parsing and successful integration of HTML, CSS, and data.

## Parallel work decisions

**Parallel:** After the field contract is agreed, Coder may create
`app/project-data.json` and initial `app/index.html` while Designer develops the visual specification
and CSS requirements. Coder may also prepare the launch structure once the app filename and server
port are fixed.

**Sequential:** CSS should be applied after the markup and class names are stable; launch and browser
preview should follow creation of all app files. Integration and final validation must occur after
HTML, CSS, JSON, and launch edits are complete.

## Edge cases

- If JavaScript fetches JSON under `file://`, the launch preview must use HTTP rather than opening
  the HTML directly. The launch server keeps the app in one origin.
- Empty or malformed JSON must not leave a blank or misleading dashboard; provide an explicit
  empty/error state.
- Missing fields, invalid status text, or missing priority values should be handled with neutral
  fallbacks and no JavaScript exception.
- Status and priority colors must not be the only indicators; use text labels.
- Long project names, owner names, or activity strings must wrap or truncate safely without breaking
  card layout.
- Narrow viewports must stack cards, preserve readable spacing, and avoid horizontal page overflow.
- Port 5500 may already be occupied; stop conflicting preview processes or use only the configured
  launch port if the launch contract remains deterministic.
- Strict launch JSON must contain no comments or trailing commas.

## Measurable validation expectations

All of these expectations should be met before handoff:

- `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist.
- `app/index.html` contains the exact text `Project Pulse`, references `styles.css`, references or
  loads `project-data.json`, and renders cards with the `project-card` class.
- Rendered cards visibly include status, recent activity, and priority for every project.
- `app/styles.css` contains `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, and at
  least one responsive media query or responsive layout rule.
- `app/project-data.json` passes `python3 -m json.tool app/project-data.json` and has a top-level
  `projects` array.
- Each project record contains `name`, `owner`, `status`, `recentActivity`, and `priority`; at least
  three project cards render in a normal preview.
- `.vscode/launch.json` passes `python3 -m json.tool .vscode/launch.json`, has no comments or
  trailing commas, and includes `Run Project Pulse Dashboard`.
- The launch configuration sets `cwd` to `${workspaceFolder}/app`, runs
  `python3 -m http.server 5500`, and uses `http://localhost:%s/index.html` as the ready action.
- Starting the launch opens `index.html` and shows a dashboard, not a directory listing.
- A 360 px-wide viewport and a desktop viewport show no horizontal page overflow, and card text
  remains legible.
- A keyboard-only pass reaches all interactive elements in a sensible order with visible focus.
- No console errors or unhandled JSON/rendering failures occur in the normal preview.

## Open questions

- The brief does not prescribe exact project names or sample owners, so the Coder may choose
  representative values unless Mona provides a dataset.
- The brief does not prescribe a visual color palette or brand tokens, so the Designer may select
  accessible neutral and status colors consistent with a polished dashboard.
