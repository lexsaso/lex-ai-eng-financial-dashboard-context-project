# Regla: Naming Conventions del Dashboard Financiero

## Nombre
Naming coherente entre dominio financiero, API FastAPI y frontend React/TypeScript.

## Alcance
- Backend: backend/app/routes.py y tests en backend/tests/test_routes.py.
- Frontend: frontend/src/lib/financial-types.ts, frontend/src/lib/financial-utils.ts y frontend/src/App.tsx.
- Documentacion de endpoints en README.md y README.es.md cuando aplique.

## Justificacion
Este proyecto depende de un contrato de datos compartido. Cambios de naming en campos como create_date u operation_type rompen filtros, graficas y tests en cascada.

## Reglas accionables
1. Campos de payload API deben mantenerse en snake_case: create_date, operation_type, business_type.
2. Nombres de tipos TS y modelos Python deben reflejar el mismo concepto de negocio: FinancialMovement, MetricsSummaryItem, KPIMetrics.
3. No introducir sinonimos para una misma entidad (ejemplo prohibido: usar revenue junto con income para el mismo dato).
4. En frontend, nombres de funciones de calculo deben usar prefijos de accion claros: compute*, format*, fetch*.
5. Si se renombra un campo de dominio, el mismo commit debe actualizar:
   - modelos Pydantic,
   - tipos TS,
   - utilidades de calculo,
   - tests backend y frontend.

## Checklist rapido de cumplimiento
- El campo existe con el mismo nombre en backend y frontend.
- No hay alias temporales o compatibilidad parcial sin fecha de retiro.
- Los tests cubren el campo renombrado.
