# Project Overview

## Product Summary
- Full-stack financial dashboard built for educational and AI-agent workflows.
- Purpose: visualize financial movements and derived metrics (income, outcome, net/profit, period comparisons, anomaly alerts).
- Primary workflow: run with Docker Compose, consume backend API from a React dashboard.

## Real Evidence From Repo
- Backend API service in `backend/app/main.py` and `backend/app/routes.py`.
- Frontend app in `frontend/src/App.tsx` using reusable dashboard components.
- Local orchestration in `docker-compose.yml` exposing frontend `5173` and backend `8000`.
- Readme instructions in `README.md` and `README.es.md` align with compose-first setup.

## Product Capabilities Implemented
- Health endpoint for service readiness: `/health`.
- Financial movement listing with filters: `/api/metrics`.
- Segmented data for business models: `/api/metrics/b2b` and `/api/metrics/b2c`.
- Faceted filter metadata: `/api/metrics/facets`.
- Aggregated summaries by day/week/month: `/api/metrics/summary`.
- Top categories endpoint: `/api/metrics/categories/top`.
- Period comparison endpoint with deltas: `/api/metrics/comparison`.
- Outcome anomaly detection endpoint: `/api/metrics/alerts`.

## Domain Contract
- Shared domain fields across backend and frontend:
	- `create_date`
	- `amount`
	- `operation_type`
	- `category`
	- `business_type`
- Backend enforces contract with Pydantic response models.
- Frontend consumes and transforms this contract in `frontend/src/lib/financial-utils.ts`.
