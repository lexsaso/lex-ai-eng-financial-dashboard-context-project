# Regla: Consistencia de datos en Frontend

## Contexto
El frontend calcula KPIs y series mensuales en `frontend/src/lib/financial-utils.ts` desde el payload de `/api/metrics`.

## Reglas
- No cambiar nombres de campos (`create_date`, `operation_type`, `business_type`, etc.) sin actualizar tipos y utilidades.
- Cualquier ajuste de cálculo en `computeKPIs` o `computeMonthlyData` requiere actualizar tests de `financial-utils.test.ts`.
- Mantener orden cronológico por `YYYY-MM` en series mensuales antes de mapear labels.
- Conservar manejo explícito de división por cero en porcentajes.
- Si se cambia `VITE_API_BASE_URL`, mantener fallback funcional para desarrollo.

## Señales de regresión comunes
- Gráficas vacías por cambio de shape en API.
- KPI de profit incorrecto por filtros de tipo de operación.
- Meses desordenados al cruzar años.
