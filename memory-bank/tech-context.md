# Tech Context

## Frontend Stack
- Runtime/UI: React 19 (`react`, `react-dom`).
- Language/build: TypeScript 6 + Vite 8.
- Styling: Tailwind CSS 4 with utility composition (`clsx`, `tailwind-merge`, `class-variance-authority`).
- Charts and icons: `recharts`, `lucide-react`.
- Testing: Vitest (`vitest`, `@vitest/coverage-v8`).
- Linting: ESLint 9 with `typescript-eslint` and React hooks/refresh plugins.

## Backend Stack
- Framework: FastAPI.
- Server: `uvicorn[standard]`.
- Debug support: `debugpy`.
- Testing: `pytest`, `pytest-cov`, `httpx`.
- Data generation: deterministic mock movements via `seed=42` in routes.

## Infrastructure and Tooling
- Container orchestration: Docker Compose (`docker-compose.yml`).
- Services:
  - `frontend` built from `frontend/Dockerfile`, port `5173`.
  - `backend` built from `backend/Dockerfile`, ports `8000` and `5678`.
- Dev workflow favors containerized startup: `docker compose up --build`.

## Key Dependency Notes
- Backend dependencies are currently unpinned in `backend/requirements.txt` (version drift risk).
- Frontend dependencies are semver-ranged in `frontend/package.json`.
- Shared contract is type-enforced in backend (Pydantic) and mirrored in frontend TS types.
