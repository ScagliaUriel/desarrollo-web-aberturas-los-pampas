# Modelo Entidad-Relación

## Diagrama
El código PlantUML del modelo se encuentra en `diagramas/er.puml`.

---

## Entidades principales

| Entidad | Descripción | Relaciones clave |
|---------|-------------|------------------|
| **Usuario** | Almacena datos personales, accesos y perfil comercial (minorista/mayorista). | Pertenece a un `Rol`. Posee muchos `Pedido` y `SolicitudCotizacion`. |
| **Producto** | Registra las aberturas del catálogo con sus precios, stock y especificaciones. | Pertenece a una `Categoria` y un `Proveedor`. Se relaciona con `DetallePedido` y `DetalleOrdenCompra`. |
| **SolicitudCotizacion** | Guarda las solicitudes de aberturas a medida con dimensiones, tipología, material, vidrio, color, observaciones, precio estimado y plano opcional. | Asociada a un `Usuario` cliente. Vinculada opcionalmente a un `Pedido` cuando se aprueba. |
| **Pedido** | Registra la cabecera de la transacción de compra, estado de pago y envío. | Pertenece a un `Usuario`. Contiene varios `DetallePedido` y opcionalmente una `Instalacion`. |
| **DetallePedido** | Almacena los ítems comprados conservando el precio histórico de la operación. | Asocia un `Pedido` con un `Producto`. |
| **Instalacion** | Modela el servicio adicional de colocación de aberturas contratado para un pedido. | Relación de 1 a 1 opcional con `Pedido`. |
| **OrdenCompra** | Documenta los pedidos de reabastecimiento enviados a los fabricantes. | Relacionada a un `Proveedor` y compuesta por varios `DetalleOrdenCompra`. |
| **DetalleOrdenCompra** | Almacena las cantidades y precios de costo de los productos solicitados al proveedor. | Asocia una `OrdenCompra` con un `Producto`. |
| **LogAuditoria** | Registra los eventos críticos del sistema (cambios de stock, precios y anulaciones) con referencia al registro afectado y su valor previo/nuevo. | Registra las acciones realizadas por cada `Usuario`. |

---

## Decisiones de diseño

### Decisión 1 — Modelado de `SolicitudCotizacion` y uso del atributo `a_medida` en `Producto`
* **Planteo:** Se analizó si las cotizaciones a medida debían ser guardadas como productos estándar o en una entidad aislada.
* **Decisión:** Se creó la entidad independiente `SolicitudCotizacion` para gestionar el ciclo de revisión técnica y presupuestación, incorporando `tipologia`, `color`, `observaciones`, `precio_estimado` y `url_plano` como datos relevantes de la solicitud. Se mantuvo la bandera booleana `a_medida` en la entidad `Producto` exclusivamente como un filtro rápido de catálogo para indicar qué modelos estándar aceptan solicitudes de modificación dimensional.

### Decisión 2 — Asociación de `Instalacion` a nivel de `Pedido` (Cabecera)
* **Planteo:** Se evaluó si la instalación debía cobrarse e indicarse por cada ventana/puerta o por la compra general.
* **Decisión:** Se modeló la entidad `Instalacion` vinculada directamente a la cabecera de `Pedido` (`||--o|`).
* **Justificación:** La logística y el equipo técnico realizan una única visita en el domicilio para colocar el lote completo de aberturas adquiridas en dicha transacción.

### Decisión 3 — Conversión de `SolicitudCotizacion` aprobada a `Pedido`
* **Planteo:** Definir cómo el cliente concreta la compra tras la aprobación del presupuesto a medida.
* **Decisión:** Se incorporó la clave foránea opcional `id_cotizacion` en la tabla `Pedido`.
* **Justificación:** Permite trazabilidad directa entre la cotización aceptada y la orden de compra e-commerce generada.

### Decisión 4 — Control de Stock Balance vs. Movimientos de Auditoría
* **Planteo:** Se debatió entre calcular el stock dinámicamente sumando/restando transacciones o mantener un atributo balance.
* **Decisión:** Se conservó el campo `stock_actual` en `Producto` con actualización atómica en BD, complementado por la entidad `LogAuditoria` con referencia a `id_registro`, `valor_anterior` y `valor_nuevo`.
* **Justificación:** Garantiza velocidad de respuesta en la vista de catálogo (< 3 segundos) reduciendo la sobrecarga de cómputo en consultas concurrentes y permite reconstruir el cambio de stock con trazabilidad precisa.