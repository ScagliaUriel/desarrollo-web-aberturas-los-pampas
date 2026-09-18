# Casos de uso

## Diagrama general

El código PlantUML del diagrama general se encuentra guardado en `diagramas/casos-de-uso.puml`.

### Actores identificados
- **Cliente (Minorista / Mayorista):** Actor principal. Navega el catálogo, realiza compras online y solicita presupuestos a medida.
- **Vendedor:** Actor interno. Gestiona cotizaciones especiales y emite órdenes de compra.
- **Encargado de Depósito:** Actor interno. Administra el inventario y despacha pedidos.
- **Administrador:** Actor interno. Posee control global de usuarios, roles y auditoría.
- **Pasarela de Pago (Mercado Pago):** Sistema externo. Procesa y valida las transacciones bancarias.

---

## CU-06 — Realizar Compra Online (Checkout)

| Campo | Detalle |
|-------|---------|
| Identificador | CU-06 |
| Nombre | Realizar Compra Online |
| Descripción | El cliente selecciona productos del carrito, confirma la dirección de envío y procede a la instancia de pago. |
| Actores | Principal: Cliente / Secundario: Pasarela de Pago |
| Precondiciones | El cliente debe autenticarse y disponer de al menos un producto en el carrito de compras. |
| Postcondiciones | Éxito: Se genera la orden de compra en estado "Pagada" y se descuenta el stock. / Fallo: La orden no se procesa o queda "Pendiente de pago", manteniendo el stock intacto. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente presiona "Iniciar Checkout" desde el carrito de compras. | El sistema solicita confirmación del domicilio de entrega y método de envío. |
| 2 | El cliente selecciona la dirección y presiona "Ir a pagar". | El sistema invoca al caso de uso CU-07 (Procesar Pago) redireccionando a la pasarela. |
| 3 | El cliente completa los datos de pago y confirma la transacción. | El sistema recibe la notificación de cobro aprobado (Webhook), marca la orden como "Pagada" y descuenta las unidades del inventario. |
| 4 | El cliente visualiza la pantalla de confirmación. | El sistema envía la factura digital por correo electrónico. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Falta de stock al momento de confirmar | Si otro usuario compró la última unidad durante el proceso, el sistema bloquea el checkout, muestra *"Producto sin stock disponible"* y devuelve al usuario al carrito. |
| E2 | Rechazo o fallo de pago en Mercado Pago | El sistema recibe la notificación de cobro denegado, mantiene la orden en estado "Pendiente de pago" y ofrece al cliente reintentar con otro medio de cobro. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Tiempo de carga de pantalla < 2 segundos. Respuesta de la pasarela < 5 segundos. |
| Frecuencia | Alta (múltiples transacciones diarias). |
| Importancia | Alta (flujo principal de ingresos e-commerce). |
| Urgencia | Alta |

---

## CU-07 — Procesar Pago Digital

| Campo | Detalle |
|-------|---------|
| Identificador | CU-07 |
| Nombre | Procesar Pago Digital |
| Descripción | Integra la API de Mercado Pago para efectuar el cobro con tarjeta o dinero en cuenta de manera segura. |
| Actores | Principal: Cliente / Secundario: Pasarela de Pago (Mercado Pago) |
| Precondiciones | Existencia de una orden de compra generada en estado "Pendiente". |
| Postcondiciones | Éxito: La transacción se valida y retorna token de pago aprobado. / Fallo: Se registra el motivo del rechazo. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente ingresa los datos de su tarjeta o selecciona saldo disponible en Mercado Pago. | La pasarela procesa los datos cifrados mediante protocolo seguro. |
| 2 | La pasarela emite la respuesta de operación autorizada. | El sistema recibe el webhook de confirmación e impacta el pago en la base de datos. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Fondos insuficientes o tarjeta rechazada | La pasarela retorna un código de error. El sistema muestra *"Pago rechazado por la entidad emisora"* sin cancelar el pedido. |
| E2 | Caída o timeout del servicio externo | Si Mercado Pago no responde en 10 segundos, el sistema muestra *"Servicio de pago no disponible temporalmente"* y guarda el intento para posterior reintento. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Respuesta de integración por API < 3 segundos. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-13 — Emitir Orden de Compra a Proveedor

| Campo | Detalle |
|-------|---------|
| Identificador | CU-13 |
| Nombre | Emitir Orden de Compra a Proveedor |
| Descripción | Permite al administrador o vendedor generar una solicitud de reposición de mercadería hacia los fabricantes. |
| Actores | Principal: Vendedor / Administrador |
| Precondiciones | El proveedor debe estar dado de alta y activo en la base de datos. |
| Postcondiciones | Éxito: Se genera el documento de Orden de Compra en estado "Enviada". / Fallo: No se emite la orden. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El usuario selecciona un proveedor del listado y presiona "Nueva Orden de Compra". | El sistema despliega el formulario con los productos asociados a dicho proveedor. |
| 2 | El usuario especifica las cantidades de aberturas a solicitar y confirma. | El sistema registra la orden de compra N° X en estado "Pendiente de entrega" y genera el archivo PDF. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Producto discontinuado o no disponible en proveedor | Si se intenta solicitar un producto dado de baja por el proveedor, el sistema notifica *"El artículo X ya no es suministrado por este proveedor"* e impide su inclusión. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Generación y registro del documento < 2 segundos. |
| Frecuencia | Media (semanal / quincenal). |
| Importancia | Media |
| Urgencia | Media |