# Tech Context

## Backend
- Dependencias: fastapi, uvicorn, pytest, httpx.
- Generación de datos mock determinística con `seed=42` en endpoints.
- Endpoints principales:
  - `/api/metrics`
  - `/api/metrics/b2b`
  - `/api/metrics/b2c`
  - `/api/metrics/facets`
  - `/api/metrics/summary`
  - `/api/metrics/categories/top`
  - `/api/metrics/comparison`
  - `/api/metrics/alerts`

## Frontend
- React 19 + TypeScript 6 + Tailwind CSS 4 + Recharts.
- Cálculo de KPIs y series en `frontend/src/lib/financial-utils.ts`.
- Tests unitarios de utilidades con Vitest.
