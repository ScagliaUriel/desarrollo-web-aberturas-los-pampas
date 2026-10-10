# Definition of Ready (DoR)

---

## Checklist del equipo

| # | Ítem | Justificación |
|---|------|---------------|
| 1 | La historia sigue el formato estándar: "Como [rol], quiero [acción], para [beneficio]". | Evita ambigüedades sobre el rol del cliente/usuario y asegura el valor comercial explicitado. |
| 2 | Cuenta con criterios de aceptación explícitos en formato Dado/Cuando/Entonces. | Establece condiciones de aprobación objetivas para QA y desarrollo sin libre interpretación. |
| 3 | Las dependencias técnicas y funcionales están identificadas y resueltas. | Previene bloqueos en medio del sprint por falta de credenciales o endpoints. |
| 4 | Los requerimientos de interfaz y maquetados (wireframes) están creados y aprobados. | Garantiza que el maquetador/desarrollador no deba adivinar la distribución visual. |
| 5 | La historia ha sido estimada en puntos de historia (Story Points) por el equipo. | Acomoda la carga de trabajo a la capacidad real del equipo según su velocidad. |
| 6 | Los 6 criterios del principio INVEST se evalúan con su observación. | Asegura que la historia sea autónoma, negociable, abordable y testeable. |
| 7 | Se identifican datos de entrada, validaciones y mensajes de error (excepciones). | Evita omitir el tratamiento de fallas y mensajes de validación para el usuario. |
| 8 | Los requisitos no funcionales (RNF) aplicables están identificados. | Protege las métricas de rendimiento, seguridad y accesibilidad requeridas. |

---

## Aplicación a historias propias

### Historia 1 — HU-03: Consulta y filtrado de aberturas en el catálogo

| Ítem | ¿Pasa? | Qué le falta (si no pasa) |
|------|--------|---------------------------|
| 1 | **Sí** | Estructurada según el formato estándar. |
| 2 | **Sí** | Cuenta con 2 criterios de aceptación Dado/Cuando/Entonces. |
| 3 | **Sí** | Estructura de base de datos de productos resuelta. |
| 4 | **Sí** | Wireframe disponible en `diagramas/wireframes/01-home-catalogo.svg`; la vista actual muestra productos destacados y CTA principal. |
| 5 | **Sí** | Estimada en 3 Story Points. |
| 6 | **Sí** | Se detalló la tabla INVEST con observaciones individuales. |
| 7 | **Sí** | Especifica la excepción con el mensaje *"No se encontraron aberturas que coincidan con la búsqueda"*. |
| 8 | **Sí** | Asocia el RNF-01 (tiempo de respuesta de carga menor a 3 segundos). |

---

### Historia 2 — HU-05: Pago digital de compras y emisión de comprobante

| Ítem | ¿Pasa? | Qué le falta (si no pasa) |
|------|--------|---------------------------|
| 1 | **Sí** | Formato de historia definido correctamente. |
| 2 | **Sí** | Especifica escenarios de pago aprobado y rechazado. |
| 3 | **Sí** | Credenciales de entorno Sandbox de Mercado Pago generadas. |
| 4 | **Sí** | Wireframe disponible en `diagramas/wireframes/04-checkout-pago.svg`. |
| 5 | **Sí** | Estimada en 8 Story Points. |
| 6 | **Sí** | Matriz INVEST evaluada con las observaciones correspondientes. |
| 7 | **Sí** | Contempla la excepción de pago rechazado dejando el pedido en "Pendiente de pago". |
| 8 | **Sí** | Asocia el RNF-07 (comunicación mediante protocolo seguro HTTPS). |

---

### Historia 3 — HU-04: Solicitud de cotización de aberturas a medida

| Ítem | ¿Pasa? | Qué le falta (si no pasa) |
|------|--------|---------------------------|
| 1 | **Sí** | Formato estándar respetado. |
| 2 | **Sí** | Define los criterios de aceptación para casos válidos e inválidos. |
| 3 | **Sí** | No presenta dependencias externas bloqueantes. |
| 4 | **Sí** | Wireframe disponible en `diagramas/wireframes/11-cotizacion-a-medida.svg`; la vista actual refleja tipología, dimensiones, vidrio y resumen de cotización. |
| 5 | **Sí** | Estimada en 5 Story Points. |
| 6 | **No** | El criterio "Pequeña" dio "No" por exigir validaciones, estados de cotización y flujo de revisión. |
| 7 | **Sí** | Define el mensaje *"Las dimensiones están fuera del rango estándar de fabricación"*. |
| 8 | **Sí** | Asocia el RNF-11 (accesibilidad y validaciones táctiles). |