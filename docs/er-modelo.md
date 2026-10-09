# Modelo Entidad-Relación

## Diagrama
El código PlantUML del modelo se encuentra en `diagramas/er.puml`[cite: 31].

---

## Entidades principales

| Entidad | Descripción | Relaciones clave |
|---------|-------------|------------------|
| **Usuario** | Almacena datos personales, accesos y perfil comercial (minorista/mayorista)[cite: 31]. | Pertenece a un `Rol`. Posee muchos `Pedido` y `SolicitudCotizacion`[cite: 31]. |
| **Producto** | Registra las aberturas del catálogo con sus precios, stock y especificaciones[cite: 31]. | Pertenece a una `Categoria` y un `Proveedor`. Se relaciona con `DetallePedido` y `DetalleOrdenCompra`[cite: 30, 31]. |
| **SolicitudCotizacion** | Guarda las solicitudes de aberturas a medida con dimensiones, materiales y planos adjuntos[cite: 31]. | Asociada a un `Usuario` cliente. Vinculada opcionalmente a un `Pedido` cuando se aprueba[cite: 30, 31]. |
| **Pedido** | Registra la cabecera de la transacción de compra, estado de pago y envío[cite: 31]. | Pertenece a un `Usuario`. Contiene varios `DetallePedido` y opcionalmente una `Instalacion`[cite: 31]. |
| **DetallePedido** | Almacena los ítems comprados conservando el precio histórico de la operación[cite: 31]. | Asocia un `Pedido` con un `Producto`[cite: 31]. |
| **Instalacion** | Modela el servicio adicional de colocación de aberturas contratado para un pedido[cite: 31]. | Relación de 1 a 1 opcional con `Pedido`[cite: 31]. |
| **OrdenCompra** | Documenta los pedidos de reabastecimiento enviados a los fabricantes[cite: 31]. | Relacionada a un `Proveedor` y compuesta por varios `DetalleOrdenCompra`[cite: 30, 31]. |
| **DetalleOrdenCompra** | Almacena las cantidades y precios de costo de los productos solicitados al proveedor[cite: 30, 31]. | Asocia una `OrdenCompra` con un `Producto`[cite: 30, 31]. |
| **LogAuditoria** | Registra los eventos críticos del sistema (cambios de stock, precios y anulaciones)[cite: 30, 31]. | Registra las acciones realizadas por cada `Usuario`[cite: 30, 31]. |

---

## Decisiones de diseño

### Decisión 1 — Modelado de `SolicitudCotizacion` y uso del atributo `a_medida` en `Producto`
* **Planteo:** Se analizó si las cotizaciones a medida debían ser guardadas como productos estándar o en una entidad aislada[cite: 31].
* **Decisión:** Se creó la entidad independiente `SolicitudCotizacion` para gestionar el ciclo de revisión técnica y presupuestación[cite: 30, 31]. Se mantuvo la bandera booleana `a_medida` en la entidad `Producto` exclusivamente como un filtro rápido de catálogo para indicar qué modelos estándar aceptan solicitudes de modificación dimensional[cite: 30, 31].

### Decisión 2 — Asociación de `Instalacion` a nivel de `Pedido` (Cabecera)
* **Planteo:** Se evaluó si la instalación debía cobrarse e indicarse por cada ventana/puerta o por la compra general[cite: 31].
* **Decisión:** Se modeló la entidad `Instalacion` vinculada directamente a la cabecera de `Pedido` (`||--o|`)[cite: 31].
* **Justificación:** La logística y el equipo técnico realizan una única visita en el domicilio para colocar el lote completo de aberturas adquiridas en dicha transacción[cite: 31].

### Decisión 3 — Conversión de `SolicitudCotizacion` aprobada a `Pedido`
* **Planteo:** Definir cómo el cliente concreta la compra tras la aprobación del presupuesto a medida[cite: 30, 31].
* **Decisión:** Se incorporó la clave foránea opcional `id_cotizacion` en la tabla `Pedido`[cite: 30, 31].
* **Justificación:** Permite trazabilidad directa entre la cotización aceptada y la orden de compra e-commerce generada[cite: 30, 31].

### Decisión 4 — Control de Stock Balance vs. Movimientos de Auditoría
* **Planteo:** Se debatió entre calcular el stock dinámicamente sumando/restando transacciones o mantener un atributo balance[cite: 30, 31].
* **Decisión:** Se conservó el campo `stock_actual` en `Producto` con actualización atómica en BD[cite: 31], complementado por la entidad `LogAuditoria`[cite: 30, 31].
* **Justificación:** Garantiza velocidad de respuesta en la vista de catálogo (< 3 segundos) reduciendo la sobrecarga de cómputo en consultas concurrentes[cite: 31].