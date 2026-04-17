# Regla: Flujo de validación obligatorio

## Orden recomendado
1. Validar backend (`pytest`) cuando se toquen rutas o utilidades Python.
2. Validar frontend (`npm test`) cuando se toquen cálculos, tipos o componentes de dashboard.
3. Confirmar arranque integrado con `docker compose up --build` para cambios full-stack.

## Comandos
- Backend: `cd backend && pytest -q`
- Frontend: `cd frontend && npm test -- --run`
- Integración: `docker compose up --build`

## Criterio de cierre
No cerrar cambios con tests rotos o sin explicar explícitamente por qué no pudieron ejecutarse en el entorno actual.
