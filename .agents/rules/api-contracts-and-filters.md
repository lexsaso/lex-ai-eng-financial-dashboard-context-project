# Regla: Contrato API y Consistencia de Filtros

## Nombre
Contrato estable para /api/metrics* con filtros consistentes entre endpoints.

## Alcance
- Endpoints en backend/app/routes.py:
  - /api/metrics
  - /api/metrics/b2b
  - /api/metrics/b2c
  - /api/metrics/facets
  - /api/metrics/summary
  - /api/metrics/categories/top
  - /api/metrics/comparison
  - /api/metrics/alerts

## Justificacion
El frontend consume varias vistas de metricas y depende de que los filtros compartan semantica. Inconsistencias generan discrepancias entre KPIs y graficas.

## Reglas accionables
1. start_date y end_date deben seguir semantica inclusiva en todos los endpoints que acepten rango.
2. Si se agrega un filtro nuevo (ejemplo: business_type), evaluar aplicarlo en todos los endpoints equivalentes o justificar por que no aplica.
3. Respuestas de movimientos deben salir ordenadas cronologicamente.
4. Limites de query params deben validarse en Query (ejemplo actual: limit ge=1, le=20).
5. Mantener salida deterministica de mocks con seed=42 para evitar pruebas flaky.

## Criterios de aceptacion por cambio
- Contrato response_model actualizado y compatible.
- Tests de rutas afectados actualizados.
- README/README.es actualizados si cambia comportamiento publico.
