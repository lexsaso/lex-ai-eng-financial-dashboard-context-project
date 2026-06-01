# Fase 1: Inventario tecnico del repositorio

## Objetivo
Documentar la estructura real del dashboard financiero y los archivos de inicializacion/operacion clave para acelerar onboarding y evaluacion.

## Mapa de carpetas (raiz)
- backend/
- frontend/
- memory-bank/
- .agents/rules/
- .agents/skills/
- README.md
- README.es.md
- docker-compose.yml
- AGENTS.md
- context.md

## Inventario por modulo

| Area | Ruta | Rol tecnico | Criticidad |
|---|---|---|---|
| Orquestacion | docker-compose.yml | Levanta frontend y backend con puertos y volumenes de desarrollo | Alta |
| Producto/arranque | README.md | Guía principal de ejecución local y contexto del proyecto | Alta |
| Producto/arranque | README.es.md | Guía equivalente en español para setup local | Media |
| Reglas de agentes | AGENTS.md | Instrucciones obligatorias para agentes sobre reglas, skills y memoria | Alta |
| Backend entrypoint | backend/app/main.py | Inicializa FastAPI, CORS e incluye rutas API | Alta |
| Backend API | backend/app/routes.py | Define modelos y endpoints de métricas financieras | Alta |
| Backend dependencias | backend/requirements.txt | Lista dependencias Python necesarias para ejecutar/testear backend | Alta |
| Backend tests | backend/tests/test_routes.py | Pruebas de endpoints y reglas clave de negocio | Alta |
| Frontend manifest | frontend/package.json | Scripts de dev/build/test y dependencias de UI/tooling | Alta |
| Frontend entrypoint | frontend/src/main.tsx | Montaje de React y carga de estilos base | Alta |
| Frontend app shell | frontend/src/App.tsx | Flujo de carga de datos, estado y composición del dashboard | Alta |
| Frontend tipos | frontend/src/lib/financial-types.ts | Contrato tipado compartido para movimientos/KPIs | Alta |
| Frontend logica | frontend/src/lib/financial-utils.ts | Calculo de KPIs y agregacion mensual | Alta |
| Frontend tests | frontend/src/lib/financial-utils.test.ts | Pruebas unitarias de calculos y formateadores | Media |
| Memoria de proyecto | memory-bank/project-overview.md | Resumen funcional del producto con evidencia real | Media |
| Memoria de proyecto | memory-bank/tech-context.md | Stack tecnologico y tooling del repositorio | Media |
| Memoria de proyecto | memory-bank/current-status.md | Estado actual, gaps y prioridades | Media |

## Archivos de inicializacion clave

### Backend
1. backend/app/main.py
2. backend/app/routes.py
3. backend/requirements.txt

### Frontend
1. frontend/package.json
2. frontend/src/main.tsx
3. frontend/src/App.tsx

### Infraestructura
1. docker-compose.yml

## Scripts y comandos operativos principales

### Frontend (package.json)
- npm run dev
- npm run build
- npm run lint
- npm run test
- npm run test:coverage

### Backend
- pytest -q

### Full stack
- docker compose up --build

## Notas de contexto real (no genericas)
1. El backend expone endpoints de métricas, facetas, resumen temporal, top categorías, comparación y alertas.
2. El frontend consume principalmente /api/metrics y deriva KPIs/charts desde utilidades tipadas.
3. Existen pruebas backend amplias de rutas y pruebas frontend focalizadas en utilidades.
4. El flujo recomendado del proyecto es compose-first (frontend 5173, backend 8000).

## Criterio de mantenimiento
Si se agrega una nueva carpeta de dominio o cambia un archivo de inicialización, actualizar este inventario en el mismo cambio.
