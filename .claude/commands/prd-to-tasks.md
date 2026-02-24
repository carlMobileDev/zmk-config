# PRD to Tasktui Tasks

Break a PRD (Product Requirements Document) into individual tasktui task files.

## Input

The user will provide either:
- A file path to a PRD document (markdown, text, etc.)
- PRD content pasted directly

Read the PRD content first, then proceed.

## How to create tasks

Each task is a markdown file in `.tasktui/tasks/` with YAML frontmatter. Use the CLI to create tasks:

```
tasktui add "Task title" --priority p1 --tags "tag1,tag2" --body "## Description

Detailed description of what needs to be done.

## Acceptance Criteria

- [ ] First criterion
- [ ] Second criterion

## Notes

Any additional context."
```

Priority levels: `p0` (urgent), `p1` (high), `p2` (medium/default), `p3` (low)

Tasks are created with status `inbox` by default. The user will promote them to `ready` via the Plan view.

**Always include a `--body` with Description, Acceptance Criteria, and Notes sections.** The body is markdown and should give enough context for someone to pick up and implement the task without referring back to the PRD.

## Rules

1. **Read the PRD thoroughly** before creating any tasks
2. **Break work into small, actionable tasks** - each task should be completable in a single focused session (1-3 hours of work)
3. **Order tasks by dependency** - create foundational tasks first so IDs reflect natural execution order
4. **Use clear imperative titles** - "Add login endpoint" not "Login endpoint" or "We need a login endpoint"
5. **Assign priority based on dependency and criticality**:
   - `p0`: Blocking foundation that everything else depends on (project setup, core data model)
   - `p1`: Core features from the PRD's must-haves
   - `p2`: Secondary features, nice-to-haves
   - `p3`: Polish, docs, cleanup
6. **Use tags** to group related tasks (e.g. `backend`, `frontend`, `auth`, `database`, `testing`)
7. **After creating all tasks**, run `tasktui list` to show the user what was created
8. **Do NOT create epic-level items** - break epics down into concrete implementation tasks
9. **Include a testing task** for each significant feature area

## Task granularity guide

Too big: "Build the authentication system"
Right size: "Add JWT token generation endpoint", "Add login form with email/password", "Add auth middleware to protect routes"

Too small: "Create auth directory"
Right size: "Set up auth module with user model and migration"

## Output

After creating tasks, display a summary table and suggest the user run `tasktui` to open the TUI and use the Plan view (key 3) to promote tasks to their ready queue.
