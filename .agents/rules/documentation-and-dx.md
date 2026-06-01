# Regla: Documentacion y DX Operativa

## Nombre
Documentacion ejecutable y experiencia de desarrollo predecible para equipo y agentes.

## Alcance
- README.md y README.es.md.
- docker-compose.yml y variables de entorno del frontend/backend.
- Mensajes de error de carga en frontend/src/App.tsx.

## Justificacion
Este proyecto se usa como base de aprendizaje y evaluacion. Si la documentacion no refleja el comportamiento real (puertos, CORS, URL API, comandos), el costo de onboarding sube y aparecen falsos errores.

## Reglas accionables
1. Todo cambio en puertos, endpoints o variables de entorno debe reflejarse en README.md y README.es.md en el mismo cambio.
2. Mantener una unica fuente de verdad para URL de API en frontend (evitar duplicar configuracion en multiples archivos).
3. Cuando exista fallback de conectividad (localhost/127.0.0.1), documentar el motivo y el contexto Docker/host.
4. Mensajes de error de UI deben ser accionables para el usuario (que revisar y donde).
5. No cerrar PR con comandos de validacion omitidos sin explicacion clara.

## Lista de verificacion DX
- docker compose up --build levanta frontend y backend.
- Endpoint /health responde 200.
- Frontend muestra estado de error entendible si API no responde.
