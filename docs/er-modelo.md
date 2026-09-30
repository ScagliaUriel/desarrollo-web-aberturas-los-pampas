# Modelo Entidad-Relación

## Diagrama
El código PlantUML del modelo se encuentra en `diagramas/er.puml`.

---

## Entidades principales

| Entidad | Descripción | Relaciones clave |
|---------|-------------|------------------|
| **Usuario** | Almacena datos personales, accesos y perfil comercial (minorista/mayorista). | Pertenece a un `Rol`. Posee muchos `Pedido` y `SolicitudCotizacion`. |
| **Producto** | Registra las aberturas del catálogo con sus precios, stock y especificaciones. | Pertenece a una `Categoria` y un `Proveedor`. Se relaciona con `DetallePedido`. |
| **SolicitudCotizacion** | Guarda las solicitudes de aberturas a medida con dimensiones, materiales y planos adjuntos. | Asociada a un `Usuario` cliente. |
| **Pedido** | Registra la cabecera de la transacción de compra, estado de pago y envío. | Pertenece a un `Usuario`. Contiene varios `DetallePedido` y opcionalmente una `Instalacion`. |
| **DetallePedido** | Almacena los ítems comprados conservando el precio histórico de la operación. | Asocia un `Pedido` con un `Producto`. |
| **Instalacion** | Modela el servicio adicional de colocación de aberturas contratado para un pedido. | Relación de 1 a 1 opcional con `Pedido`. |
| **OrdenCompra** | Documenta los pedidos de reabastecimiento enviados a los fabricantes. | Relacionada a un `Proveedor`. |

---

## Decisiones de diseño

### Decisión 1 — Modelado de la entidad `SolicitudCotizacion` independiente de `Producto`
* **Planteo:** Se evaluó incluir las aberturas a medida dentro de la tabla `Producto` marcándolas con una bandera booleana.
* **Decisión:** Se creó la entidad explícita `SolicitudCotizacion` separada de `Producto`.
* **Justificación:** Las aberturas a medida no poseen stock inicial ni precio prefijado y requieren atributos específicos (`alto`, `ancho`, `tipo_vidrio`, `url_plano`) y un flujo de estados de revisión previa.

### Decisión 2 — Asociación del servicio de `Instalacion` a nivel de `Pedido` (Cabecera)
* **Planteo:** Se analizó si la instalación debía asociarse a cada ítem individual en `DetallePedido` o a la cabecera del `Pedido`.
* **Decisión:** Se modeló la entidad `Instalacion` vinculada directamente a `Pedido` (`||--o|`).
* **Justificación:** Operativamente, la visita técnica y la colocación se coordinan en un único viaje y fecha para todo el conjunto de aberturas adquiridas en el mismo pedido.

### Decisión 3 — Histórico de precios en `DetallePedido`
* **Planteo:** Se consideró calcular el total del pedido consultando el precio del `Producto`.
* **Decisión:** Se incluyó el atributo `precio_unitario` en `DetallePedido`.
* **Justificación:** Garantiza la integridad histórica de la facturación frente a futuros cambios de precios en el catálogo.