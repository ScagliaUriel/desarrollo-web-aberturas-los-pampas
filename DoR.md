# Definition of Ready (DoR)

_Antes de que una historia entre a desarrollo, tiene que pasar un filtro: el Definition of
Ready. Es un acuerdo del equipo sobre qué condiciones mínimas debe cumplir una historia para
considerarse "lista para trabajar". Si no las cumple, vuelve a refinamiento._

---

## Checklist del equipo

| # | Ítem | Justificación (qué problema evita, máx. 3 renglones) |
|---|------|--------------------------------------------------------|
| 1 | La historia sigue el formato estándar: "Como [rol], quiero [acción], para [objetivo]". | Evita la ambigüedad sobre quién realiza la acción y el valor real de negocio que aporta. |
| 2 | Cuenta con criterios de aceptación explícitos redactados en formato Dado/Cuando/Entonces. | Aclara el alcance y establece condiciones objetivas para dar por terminada la historia. |
| 3 | Las dependencias técnicas y funcionales están identificadas y resueltas previo al sprint. | Previene bloqueos durante el desarrollo por falta de integraciones o servicios requeridos. |
| 4 | Los requerimientos de interfaz, campos del formulario y comportamientos de la vista están especificados. | Garantiza que la maquetación y el desarrollo no requieran adivinar campos en el sprint. |
| 5 | La historia ha sido estimada en puntos de historia (Story Points) por el equipo. | Asegura que la tarea se adapte a la capacidad real del equipo en el ciclo de trabajo. |
| 6 | La historia respeta la validación del principio INVEST (se evalúan sus 6 criterios y se documenta la observación de cada uno). | Garantiza que las historias sean independientes, pequeñas y verificables dentro de un sprint; evita marcar "Sí" sin justificar cada criterio. |
| 7 | Se identifican los datos de entrada y los mensajes de error/validación esperados. | Cubre los flujos alternativos y de excepción antes del desarrollo, evitando que el equipo tenga que inventar mensajes o validaciones durante el sprint. |
---

## Aplicación a tres historias propias

### Historia 1 — HU-02: Consulta y filtrado de aberturas en el catálogo

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **Sí** | Estructurada correctamente con rol, acción y beneficio. |
| 2 | **Sí** | Definidos explícitamente en formato Dado/Cuando/Entonces. |
| 3 | **Sí** | El catálogo base (RF-04/05/06) ya está desarrollado como prerrequisito, así que no bloquea el filtrado. |
| 4 | **Sí** | Se definieron la barra de búsqueda y los filtros por material y categoría en el wireframe de catálogo. |
| 5 | **Sí** | Estimada en 3 Story Points por el equipo. |
| 6 | **Sí** | Los 6 criterios INVEST fueron evaluados uno por uno en `docs/historias-de-usuario.md` (HU-02); todos se cumplen. |
| 7 | **Sí** | Mensajes definidos: *"No se encontraron aberturas que coincidan con la búsqueda"* y etiqueta *"Sin stock"*. |

---

### Historia 2 — HU-04: Pago de pedidos con pasarela digital

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **Sí** | Cumple con la estructura de la plantilla oficial. |
| 2 | **Sí** | Especifica los escenarios de pago aprobado y rechazado. |
| 3 | **Sí** | Las credenciales Sandbox de Mercado Pago están creadas. |
| 4 | **Sí** | Pantalla de confirmación de pedido y redirección maquetada. |
| 5 | **Sí** | Estimada en 8 Story Points por el equipo. |
| 6 | **Sí** | Los 6 criterios INVEST fueron evaluados en `docs/historias-de-usuario.md` (HU-04); "Independiente" se justifica por no depender de otras historias, solo de que exista una orden generada. |
| 7 | **Sí** | Mensajes definidos: pago rechazado deja la orden en *"Pendiente de pago"* sin borrarla; pago aprobado dispara el envío del comprobante. |

---

### Historia 3 — HU-03: Cotización de aberturas a medida

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **Sí** | Formato de historia definido correctamente. |
| 2 | **No** | Falta definir las opciones permitidas de materiales y tipos de vidrio. |
| 3 | **Sí** | No presenta bloqueos de infraestructura. |
| 4 | **No** | Falta el maquetado del formulario de ingreso de dimensiones. |
| 5 | **No** | El equipo no pudo estimarla por falta de definición en los campos. |
| 6 | **Sí** | Aporta valor de negocio pero requiere refinamiento. |
