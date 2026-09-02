# Definition of Ready (DoR)

_Antes de que una historia entre a desarrollo, tiene que pasar un filtro: el Definition of Ready. Es un acuerdo del equipo sobre qué condiciones mínimas debe cumplir una historia para considerarse "lista para trabajar". Si no las cumple, vuelve a refinamiento._

---

## Checklist del equipo

| # | Ítem | Justificación (qué problema evita, máx. 3 renglones) |
|---|------|--------------------------------------------------------|
| 1 | La historia sigue el formato estándar: "Como [rol], quiero [acción], para [beneficio]". | Evita la ambigüedad sobre quién realiza la acción y el valor real de negocio que aporta al proyecto. |
| 2 | Cuenta con criterios de aceptación explícitos redactados en formato Given-When-Then o lista de verificación. | Evita malentendidos sobre el alcance exacto y la falta de claridad sobre cuándo la tarea se da por terminada. |
| 3 | Las dependencias técnicas y funcionales están identificadas y resueltas previo al sprint. | Evita bloqueos en pleno desarrollo al depender de otras tareas o integraciones externas no disponibles. |
| 4 | El diseño de interfaz o wireframe de la vista requerida está adjunto y aprobado. | Evita retrabajo en el maquetado frontend por interpretaciones libres de la interfaz por parte del desarrollador. |
| 5 | La historia ha sido estimada en puntos de historia (Story Points) por el equipo. | Evita sobrecargar la capacidad del equipo en el sprint por falta de dimensión del esfuerzo requerido. |
| 6 | La historia respeta el principio INVEST (independiente, negociable, valiosa, estimable, pequeña, testeable). | Evita historias épicas o gigantes que no puedan completarse dentro de un solo ciclo de trabajo. |
| 7 | Se identifican explícitamente los datos de entrada requeridos y los mensajes de error/validación esperados. | Evita omitir el tratamiento de excepciones, validaciones de formularios y fallos del sistema durante la codificación. |

---

## Aplicación a tres historias propias

### Historia 1 — HU-03: Búsqueda y filtrado de aberturas en el catálogo online

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1. Formato estándar | **Sí** | Cumple con rol, acción y beneficio. |
| 2. Criterios de aceptación | **Sí** | Definidos correctamente en formato Given-When-Then. |
| 3. Dependencias resueltas | **Sí** | Depende del catálogo base (HU-01) la cual ya está desarrollada. |
| 4. Wireframe / UI aprobado | **Sí** | Incluye el boceto de la barra de búsqueda y filtros por material. |
| 5. Estimación en puntos | **Sí** | Estimada en 3 Story Points. |
| 6. Principio INVEST | **Sí** | Es pequeña, independiente y testeable. |
| 7. Datos y validaciones | **Sí** | Especifica comportamiento ante búsquedas sin resultados. |

**Resultado final:** **LISTA PARA DESARROLLO (PASA)**

---

### Historia 2 — HU-08: Pago de compras mediante Mercado Pago

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1. Formato estándar | **Sí** | Cumple con la estructura de usuario/beneficio. |
| 2. Criterios de aceptación | **Sí** | Incluye los escenarios de pago aprobado, pendiente y rechazado. |
| 3. Dependencias resueltas | **Sí** | Credenciales Sandbox de la API de Mercado Pago creadas y configuradas. |
| 4. Wireframe / UI aprobado | **Sí** | Diseño del checkout integrado disponible. |
| 5. Estimación en puntos | **Sí** | Estimada en 8 Story Points. |
| 6. Principio INVEST | **Sí** | Aporta valor directo de negocio y es testeable en entorno de pruebas. |
| 7. Datos y validaciones | **Sí** | Especifica respuestas esperadas según códigos de error del Gateway. |

**Resultado final:** **LISTA PARA DESARROLLO (PASA)**

---

### Historia 3 — HU-11: Solicitud de presupuesto para aberturas a medida

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1. Formato estándar | **Sí** | Definida correctamente según la plantilla. |
| 2. Criterios de aceptación | **No** | Falta definir los campos obligatorios del formulario de medidas y el plazo máximo de respuesta. |
| 3. Dependencias resueltas | **Sí** | Módulo de usuarios disponible. |
| 4. Wireframe / UI aprobado | **No** | No se adjuntó el diseño de la pantalla de cotizaciones a medida. |
| 5. Estimación en puntos | **No** | El equipo no pudo estimarla por falta de definición en los requisitos del formulario. |
| 6. Principio INVEST | **Sí** | Es valiosa y de tamaño adecuado. |
| 7. Datos y validaciones | **No** | No están especificados los formatos aceptados para adjuntar planos/planillas (.pdf, .jpg). |

**Resultado final:** **RECHAZADA (VUELVE A REFINAMIENTO)**