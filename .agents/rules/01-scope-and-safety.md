# Regla: Alcance y seguridad de cambios

## Objetivo
Garantizar cambios pequeños, verificables y compatibles con el estado actual del dashboard financiero.

## Reglas
- No romper contratos existentes del backend ni del frontend sin actualizar tests en el mismo cambio.
- Evitar refactors amplios sin requerimiento explícito.
- Mantener tipos compartidos consistentes entre FastAPI y React/TypeScript.
- No introducir dependencias nuevas salvo necesidad justificada.
- Priorizar datos determinísticos para pruebas y debugging (`seed=42` en generación mock).

## Checklist rápido antes de cerrar
- ¿Se preservan rutas API actuales?
- ¿Se preserva shape de respuesta esperado por componentes?
- ¿Se tocaron solo archivos necesarios?
- ¿Hay pruebas o validación equivalente para el cambio?
