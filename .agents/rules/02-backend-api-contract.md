# Regla: Contrato de API Backend

## Contexto
El backend usa FastAPI en `backend/app/routes.py` y expone endpoints de métricas, resumen, comparación, alertas y segmentos B2B/B2C.

## Reglas de implementación
- Mantener `response_model` en cada endpoint para validar shape de salida.
- Si se agrega filtro nuevo, aplicarlo de forma consistente en endpoints equivalentes.
- Mantener orden cronológico en respuestas de movimientos (`ensure_chronological_order`).
- Mantener semántica actual de fechas inclusivas en filtros (`start_date` y `end_date`).
- Si se modifica lógica agregada (summary/top/comparison/alerts), actualizar tests en `backend/tests/test_routes.py`.

## Reglas de tests
- Tests deben cubrir status code + shape mínima + regla de negocio clave.
- Nuevos endpoints deben incluir al menos 1 caso feliz y 1 caso de filtro.
