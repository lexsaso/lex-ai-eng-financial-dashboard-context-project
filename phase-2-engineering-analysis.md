# Fase 2: Analisis de practicas de ingenieria

## Alcance
Revision de backend (FastAPI), frontend (React + TypeScript), tests, y documentacion del repositorio.

## 1) Buenas practicas implementadas (5)

### 1. Contrato tipado de API con validacion de salida
- Categoria: Arquitectura, Calidad de API
- Evidencia:
  - backend/app/routes.py:24
  - backend/app/routes.py:246
  - backend/app/routes.py:262
  - backend/app/routes.py:267
- Valor: El uso de `BaseModel` y `response_model` reduce regresiones de shape entre backend y frontend.

### 2. Semilla deterministica para datos mock
- Categoria: Testing, Reproducibilidad
- Evidencia:
  - backend/app/routes.py:95
  - backend/app/routes.py:255
  - backend/app/routes.py:265
  - backend/app/routes.py:280
- Valor: `seed=42` permite resultados estables para depuracion y pruebas.

### 3. Orden cronologico explicitamente garantizado
- Categoria: Arquitectura de datos
- Evidencia:
  - backend/app/routes.py:146
  - backend/app/routes.py:259
  - backend/tests/test_routes.py:17
  - backend/tests/test_routes.py:60
- Valor: Evita comportamientos inconsistentes en graficas y agregaciones temporales.

### 4. Cobertura de tests en rutas y reglas funcionales clave
- Categoria: Testing
- Evidencia:
  - backend/tests/test_routes.py:32
  - backend/tests/test_routes.py:72
  - backend/tests/test_routes.py:120
  - backend/tests/test_routes.py:158
- Valor: Se prueban filtros, endpoints y shape de respuesta en varios casos importantes.

### 5. Manejo defensivo de division por cero en KPI
- Categoria: Calidad de dominio, Frontend
- Evidencia:
  - frontend/src/lib/financial-utils.ts:31
  - frontend/src/lib/financial-utils.ts:61
  - frontend/src/lib/financial-utils.test.ts:46
- Valor: Evita errores numericos y resultados invalidos en condiciones de borde.

## 2) Malas practicas o riesgos tecnicos (5)

### 1. CORS permisivo con credenciales habilitadas
- Categoria: Seguridad, Arquitectura
- Evidencia:
  - backend/app/main.py:12
  - backend/app/main.py:13
  - backend/app/main.py:14
- Riesgo: `allow_origin_regex` amplio junto con `allow_credentials=True` puede aceptar origenes no deseados en entornos mal configurados.
- Impacto probable: Exposicion de cookies/sesion en escenarios de despliegue sin hardening.

### 2. Dependencias Python sin versionado fijo
- Categoria: DX, Reproducibilidad
- Evidencia:
  - backend/requirements.txt:1
- Riesgo: Cambios aguas arriba pueden romper build o tests entre ejecuciones.
- Impacto probable: Inestabilidad de entorno y debugging dificil.

### 3. Falta de tests de UI y de integracion frontend-backend
- Categoria: Testing
- Evidencia:
  - frontend/src/lib/financial-utils.test.ts:1
  - frontend/src/App.tsx:56
- Riesgo: Solo hay pruebas unitarias de utilidades; no se valida render, estados de carga/error ni contrato API en la UI.
- Impacto probable: Regresiones visuales o de flujo no detectadas.

### 4. Configuracion y fallback de API hardcodeados en cliente
- Categoria: Configuracion, Arquitectura
- Evidencia:
  - frontend/src/App.tsx:13
  - frontend/src/App.tsx:17
- Riesgo: Multiples endpoints quemados en codigo incrementan complejidad y posibilidad de inconsistencia por entorno.
- Impacto probable: Incidencias de conectividad en staging/prod y mayor deuda tecnica.

### 5. Etiqueta temporal fija en el header
- Categoria: UX, Mantenibilidad
- Evidencia:
  - frontend/src/App.tsx:81
- Riesgo: `period="2024 - Full Year"` no refleja filtros ni periodo real.
- Impacto probable: Confusion de usuarios y lectura incorrecta de datos.

## 3) Clasificacion de hallazgos

| Categoria | Buenas practicas | Riesgos |
|---|---:|---:|
| Arquitectura | 2 | 2 |
| Testing | 2 | 1 |
| Seguridad | 0 | 1 |
| DX / Reproducibilidad | 1 | 1 |
| UX / Mantenibilidad | 0 | 1 |

## 4) Estrategia: borrador de reglas para mitigar riesgos

### Regla R1: Endurecimiento de CORS por entorno
- Para `development`: permitir solo `localhost` y `127.0.0.1` explicitos.
- Para `production`: eliminar regex amplios y declarar lista cerrada de dominios.
- Si `allow_credentials=True`, prohibir comodines y regex de amplio alcance.

### Regla R2: Dependencias backend fijadas
- Versionar `backend/requirements.txt` con versiones exactas o rango acotado.
- Mantener archivo de bloqueo (si aplica) y actualizarlo solo con PR dedicado.

### Regla R3: Minimo de testing de UI
- Agregar tests para `App` con casos:
  - carga exitosa
  - error de API
  - estado loading
  - render de KPIs y charts con datos
- Cualquier cambio en fetch/estado debe incluir al menos un test de regresion.

### Regla R4: Politica de configuracion de API centralizada
- Definir una sola fuente de verdad para URL base (ej. modulo `config.ts`).
- Evitar listas de fallback hardcodeadas en componentes.
- Documentar variables de entorno y defaults en README.

### Regla R5: Metadatos de periodo dinamicos
- El texto de periodo en header debe derivarse de datos/filters (`min_date`, `max_date` o query activa).
- Prohibir periodos estaticos en componentes de dashboard salvo mocks de storybook.

### Regla R6: Checklist de cierre de PR
- Verificar contrato API (shape y tipos).
- Verificar pruebas backend y frontend.
- Confirmar que etiquetas de UI no queden hardcodeadas para datos dinamicos.

## 5) Priorizacion sugerida (quick wins)
1. R2 (versionado de dependencias) - bajo costo, alto impacto en estabilidad.
2. R5 (periodo dinamico en UI) - bajo costo, mejora inmediata de confianza.
3. R3 (tests de App) - costo medio, reduce regresiones visibles.
4. R4 (config API centralizada) - costo medio, mejora despliegues.
5. R1 (hardening CORS) - costo medio, impacto alto en seguridad.

## Estado Git para esta fase
- No se realizo commit por decision explicita del usuario durante esta sesion.
- Archivo preparado para commit dedicado cuando se autorice.
