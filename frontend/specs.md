# Especificación del Frontend

## 1. Objetivo
Definir el comportamiento esperado del frontend del dashboard financiero para asegurar consistencia visual, funcional y técnica.

## 2. Alcance
Esta especificación cubre:
- Estructura principal de la interfaz.
- Flujo de obtención y transformación de datos.
- Reglas de cálculo y visualización de KPIs y gráficas.
- Estados de carga y error.
- Criterios de aceptación funcionales.

No cubre:
- Cambios de contrato de API del backend.
- Lógica interna del motor de datos fuera de la aplicación React.

## 3. Stack y arquitectura
- Framework: React + TypeScript.
- Build: Vite.
- Estilos: sistema de componentes del proyecto y estilos globales.
- Fuente de datos principal: endpoint de métricas del backend.
- Capa de dominio en frontend: utilidades en src/lib para tipos y cálculos.

## 4. Estructura de UI esperada
La pantalla principal debe incluir:
- Encabezado del dashboard.
- Fila de KPIs con tarjetas para Income, Outcome y Profit.
- Gráfica de Income vs Outcome mensual.
- Gráfica de porcentaje de Profit.

Comportamiento responsive:
- Desktop: tarjetas y gráficas con distribución horizontal priorizando legibilidad.
- Mobile: reorganización vertical con márgenes y espaciados consistentes.

## 5. Contrato de datos consumido
El frontend espera elementos de movimientos financieros con campos compatibles con las utilidades existentes, incluyendo:
- create_date
- operation_type
- business_type
- amount

Notas:
- No renombrar campos en frontend sin actualizar tipos y utilidades asociadas.
- Se debe mantener compatibilidad con los cálculos actuales de KPIs y series mensuales.

## 6. Reglas de transformación de datos
Las utilidades de dominio deben:
- Calcular KPIs de income, outcome y profit con manejo explícito de división por cero.
- Construir series mensuales ordenadas cronológicamente en formato YYYY-MM antes de mapear labels.
- Evitar efectos colaterales y mantener funciones determinísticas.

## 7. Estados de la aplicación
Estados mínimos obligatorios:
- Loading: mostrar skeletons o placeholders mientras se carga data.
- Success: renderizar KPIs y charts con datos transformados.
- Empty: mostrar estado sin datos cuando la API responde sin registros.
- Error: mostrar mensaje claro y no bloqueante con opción de reintento.

## 8. Criterios de aceptación
1. El dashboard renderiza sin errores en desktop y mobile.
2. Los KPIs coinciden con los cálculos de utilidades para el mismo dataset.
3. Las gráficas no muestran meses desordenados al cruzar años.
4. El porcentaje de profit no rompe en casos con income igual a 0.
5. Si la API falla, la UI informa el error de forma comprensible.

## 9. Pruebas y validación
- Las utilidades financieras deben tener pruebas unitarias activas.
- Cualquier cambio en cálculos exige actualización de pruebas relacionadas.
- Validación recomendada en local:
	- npm test -- --run

## 10. Consideraciones de mantenimiento
- Mantener esta especificación actualizada cuando cambie:
	- El layout principal del dashboard.
	- Las reglas de cálculo de KPIs y series.
	- El contrato de datos consumido por el frontend.
