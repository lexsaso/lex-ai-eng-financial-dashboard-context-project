# Regla: Testing Standards para Metricas Financieras

## Nombre
Cobertura minima obligatoria por cambio de dominio, endpoint o calculo de KPI.

## Alcance
- Backend: backend/tests/test_routes.py.
- Frontend: frontend/src/lib/financial-utils.test.ts y futuros tests de App/componentes.
- Flujo local y CI usando pytest y vitest.

## Justificacion
Los errores mas costosos en este dashboard son silenciosos: numeros incorrectos, filtros incompletos o series desordenadas. Sin pruebas orientadas a reglas de negocio, estos bugs llegan a produccion.

## Reglas accionables
1. Todo cambio en backend/app/routes.py debe incluir o ajustar al menos un test en backend/tests/test_routes.py.
2. Todo cambio en computeKPIs o computeMonthlyData debe ajustar tests en frontend/src/lib/financial-utils.test.ts.
3. Nuevos endpoints de metricas requieren minimo:
   - 1 caso feliz (status + shape),
   - 1 caso de filtros,
   - 1 validacion de regla de negocio clave.
4. Si se modifica logica temporal (day/week/month), agregar caso que cruce anio para evitar orden incorrecto.
5. Si no se ejecutan pruebas en la sesion, documentar bloqueo tecnico explicitamente en el PR/entregable.

## Comandos estandar
- Backend: cd backend && pytest -q
- Frontend: cd frontend && npm test -- --run
- Integracion: docker compose up --build
