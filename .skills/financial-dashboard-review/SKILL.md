---
name: financial-dashboard-review
description: Review and change this financial dashboard using its API, UI, testing, accessibility, and delivery conventions.
---

# Financial Dashboard Project Review

## Objective
Produce evidence-based reviews and narrowly scoped changes that preserve this repository's financial API contract, dashboard behavior, and documented engineering workflow.

## Inputs
- The user's requested outcome and scope, including the current branch and intended base branch when delivery is requested.
- `AGENTS.md`, `.agents/rules/`, `.agents/skills/`, `.skills/`, and relevant files in `memory-bank/`.
- The current git status, branch, base/head diff, and nearby implementation/tests for the requested behavior.
- Relevant frontend components and utilities under `frontend/src/`, API routes and tests under `backend/`, and Docker Compose configuration when deployment or runtime behavior is involved.
- Available validation commands and environment limitations; never assume a browser, service, or dependency is available without checking.

## Outputs
- Prioritized findings or a concise change summary with repository-relative file references.
- A list of files changed and the reason each file is in scope.
- Exact validation commands, observed results, warnings, and checks that could not run.
- For delivery requests, a descriptive commit and PR summary naming the head and base branches; never claim a push or PR succeeded until confirmed by the remote/tool result.

## Acceptance Criteria
- Financial API changes preserve typed response models, field names (`create_date`, `amount`, `operation_type`, `category`, `business_type`), inclusive date filters, chronological ordering, and deterministic mock data (`seed=42`); update `backend/tests/test_routes.py` and run `cd backend && pytest -q` when relevant.
- Financial calculation changes preserve chronological `YYYY-MM` aggregation and division-by-zero behavior; update `frontend/src/lib/financial-utils.test.ts` and run `cd frontend && npm test -- --run` when relevant.
- Dashboard UI changes use semantic headings and native controls, provide accessible names or text alternatives for meaningful visuals, keep decorative icons out of the accessibility tree, maintain visible keyboard focus, and assess contrast against WCAG AA thresholds (4.5:1 normal text, 3:1 large text and non-text UI). Charts must have a keyboard path and a textual summary of their data.
- Frontend changes pass `cd frontend && npm run lint` and `cd frontend && npm run build`; report, rather than hide, existing warnings such as the Vite bundle-size warning.
- Full-stack or deployment changes validate with `docker compose config --quiet` and, when available, `docker compose up --build`; record environment blockers precisely.
- Update `memory-bank/progress.md` with the actual branch state, validation results, known warnings, and accessibility limitations; never claim full WCAG conformance from static checks alone.
- Keep commits limited to the requested, reviewed scope; preserve unrelated worktree changes, never commit secrets, and target `main` for PRs when requested.
