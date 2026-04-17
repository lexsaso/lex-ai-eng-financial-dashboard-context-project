# Skill: Evaluación del repositorio financiero

## Cuándo usar
Usar esta skill cuando se pida "evaluar los archivos", auditar el estado del proyecto o preparar reglas/memoria para agentes.

## Entradas mínimas
- Estructura del repo.
- Archivos clave de backend (`backend/app/*.py`, `backend/tests/*.py`).
- Archivos clave de frontend (`frontend/src/lib/*.ts`, `frontend/src/App.tsx`).
- README(s) y AGENTS.

## Procedimiento
1. Leer AGENTS y README para extraer requisitos de trabajo.
2. Verificar que exista `.agents/rules`, `.agents/skills` y `memory-bank`.
3. Inspeccionar backend:
   - Endpoints públicos y modelos.
   - Funciones de filtrado/agregación.
   - Cobertura de pruebas para rutas críticas.
4. Inspeccionar frontend:
   - Tipos de datos financieros.
   - Utilidades de cálculo y pruebas.
   - Consumo de API en `App.tsx`.
5. Generar salida:
   - Hallazgos concretos.
   - Reglas accionables (no genéricas).
   - Estado de validación (tests ejecutados o bloqueo técnico).

## Formato de salida recomendado
- Hallazgos (priorizados).
- Cambios aplicados.
- Riesgos abiertos.
- Siguientes pasos concretos.
