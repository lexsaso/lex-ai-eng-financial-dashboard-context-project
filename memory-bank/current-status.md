# Current Status

## Implemented Features
- Backend API with 8 domain endpoints plus `/health`.
- Deterministic financial mock generation (`seed=42`) with B2B/B2C segmentation.
- Inclusive date filtering and category/operation filters in movement endpoints.
- Aggregation features:
	- summary by day/week/month,
	- top categories,
	- period comparison with absolute and percentage delta,
	- outcome anomaly alerts based on baseline threshold.
- Frontend dashboard renders:
	- KPI row (income/outcome/profit),
	- income vs outcome chart,
	- profit percent chart,
	- loading and error states.

## Validation Coverage Today
- Backend tests in `backend/tests/test_routes.py` cover route status, shape, filters, and core business rules.
- Frontend tests in `frontend/src/lib/financial-utils.test.ts` cover KPI calculations, chronological monthly aggregation, and formatters.

## Known Gaps
- No dedicated UI/integration tests for `frontend/src/App.tsx` data-fetch flow.
- Backend dependency versions are not pinned in `backend/requirements.txt`.
- API base URL fallback logic is currently embedded in `frontend/src/App.tsx` instead of a centralized config module.
- Dashboard period label is hardcoded (`2024 - Full Year`) and not derived from active data range.

## Next Priorities
1. Add frontend app-level tests for loading/success/error API states.
2. Pin backend dependencies to improve reproducibility across environments.
3. Centralize API base URL configuration and document environment behavior.
4. Make period label dynamic from selected/available date range.
5. Keep rules and memory-bank aligned after each phase commit.

## Operational Commands
- Backend tests: `cd backend && pytest -q`
- Frontend tests: `cd frontend && npm test -- --run`
- Full stack check: `docker compose up --build`
