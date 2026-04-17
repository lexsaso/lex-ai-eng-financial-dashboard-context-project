# Conventions

- Mantener contrato de campos financieros compartidos entre backend y frontend.
- Preservar orden cronológico de movimientos y agregados temporales.
- Evitar división por cero en cálculos porcentuales.
- Cambios en lógica financiera requieren ajuste de tests asociados.
- En respuestas API, usar modelos tipados (`response_model`) para estabilidad del contrato.
