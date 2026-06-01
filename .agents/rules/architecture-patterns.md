# Regla: Patrones de Arquitectura del Dashboard

## Nombre
Separacion clara entre capa de datos (backend), transformacion (utils) y presentacion (componentes).

## Alcance
- Backend: endpoints y logica de agregacion en backend/app/routes.py.
- Frontend: orquestacion en frontend/src/App.tsx y calculos en frontend/src/lib/financial-utils.ts.
- Componentes de dashboard en frontend/src/components/dashboard/.

## Justificacion
La arquitectura actual funciona porque los calculos de negocio no estan mezclados con la UI. Si se rompe esta separacion, se incrementan regresiones y se dificulta testear.

## Reglas accionables
1. En backend, toda logica de filtrado y agregacion debe vivir en funciones reutilizables, no inline dentro de endpoints.
2. En frontend, App.tsx solo orquesta fetch/estado; los calculos financieros van en financial-utils.ts.
3. Componentes visuales (charts/cards/header) no deben recalcular KPIs complejos; solo reciben props procesadas.
4. Cualquier endpoint nuevo de metricas debe definir response_model explicito.
5. Mantener orden cronologico antes de exponer series temporales (backend: ensure_chronological_order; frontend: sort por YYYY-MM).

## Antipatrones prohibidos
- Parsear y agregar datos financieros dentro de componentes de grafica.
- Duplicar filtros de fecha con logica distinta entre endpoints equivalentes.
- Saltarse tipos compartidos para enviar objetos anonimos sin contrato.
