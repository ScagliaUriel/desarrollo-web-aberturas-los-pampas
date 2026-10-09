# Casos de uso

## Diagrama general

El código PlantUML del diagrama general se encuentra guardado en `diagramas/casos-de-uso.puml`[cite: 31].

### Actores identificados
- **Cliente:** Actor principal externo. Navega el catálogo, realiza compras online y solicita presupuestos de aberturas a medida[cite: 31].
- **Cliente Registrado:** Actor principal autenticado. Realiza el checkout y efectúa el pago mediante la pasarela digital[cite: 30, 31].
- **Gestor de Ventas:** Actor interno. Revisa y gestiona solicitudes de cotización a medida y atiende reclamos comerciales[cite: 30, 31].
- **Operador de Depósito:** Actor interno. Controla el inventario, emite Órdenes de Compra y coordina las fechas de instalación técnica[cite: 30, 31].
- **Mercado Pago:** Pasarela de pago externa. Procesa los cobros con tarjeta o saldo virtual[cite: 30, 31].

### Justificación de Relaciones UML Especificadas
- **`CU-03 (Solicitar Cotización a Medida) <<extend>> CU-02 (Consultar Catálogo)`:** La relación de extensión se justifica ya que la solicitud a medida es un flujo opcional que el cliente activa únicamente si las aberturas estándar ofrecidas en el catálogo no satisfacen sus requerimientos de dimensiones o acabados[cite: 30, 31].
- **`CU-05 (Procesar Pago Digital) <<include>> CU-04 (Realizar Checkout)`:** La inclusión es obligatoria dado que no es posible finalizar la confirmación de la orden de compra en el e-commerce sin invocar y aprobar el cobro electrónico mediante la pasarela[cite: 30, 31].

---

## CU-04 — Realizar Compra Online (Checkout)

| Campo | Detalle |
|-------|---------|
| Identificador | CU-04 |
| Nombre | Realizar Compra Online |
| Descripción | El cliente selecciona productos del carrito, confirma la dirección de envío y procede a la instancia de pago[cite: 31]. |
| Actores | Principal: Cliente Registrado / Secundario: Mercado Pago[cite: 30, 31] |
| Precondiciones | El cliente debe autenticarse y disponer de al menos un producto en el carrito de compras[cite: 31]. |
| Postcondiciones | Éxito: Se genera la orden de compra en estado "Pagada" y se descuenta el stock[cite: 31]. / Fallo: La orden no se procesa o queda "Pendiente de pago", manteniendo el stock intacto[cite: 31]. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente presiona "Iniciar Checkout" desde el carrito de compras[cite: 31]. | El sistema solicita confirmación del domicilio de entrega y método de envío[cite: 31]. |
| 2 | El cliente selecciona la dirección y presiona "Ir a pagar"[cite: 31]. | El sistema invoca al caso de uso CU-05 (Procesar Pago Digital) redireccionando a la pasarela[cite: 31]. |
| 3 | El cliente completa los datos de pago y confirma la transacción[cite: 31]. | El sistema recibe la notificación de cobro approved (Webhook), marca la orden como "Pagada" y descuenta las unidades del inventario[cite: 31]. |
| 4 | El cliente visualiza la pantalla de confirmación[cite: 31]. | El sistema envía la factura digital por correo electrónico[cite: 31]. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Falta de stock al momento de confirmar | Si otro usuario compró la última unidad durante el proceso, el sistema bloquea el checkout, muestra *"Producto sin stock disponible"* y devuelve al usuario al carrito[cite: 31]. |
| E2 | Rechazo o fallo de pago en Mercado Pago | El sistema recibe la notificación de cobro denegado, mantiene la orden en estado "Pendiente de pago" y ofrece al cliente reintentar con otro medio de cobro[cite: 31]. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Tiempo de carga de pantalla < 2 segundos. Respuesta de la pasarela < 5 segundos[cite: 31]. |
| Frecuencia | Alta (múltiples transacciones diarias)[cite: 31]. |
| Importancia | Alta (flujo principal de ingresos e-commerce)[cite: 31]. |
| Urgencia | Alta[cite: 31] |

---

## CU-05 — Procesar Pago Digital

| Campo | Detalle |
|-------|---------|
| Identificador | CU-05 |
| Nombre | Procesar Pago Digital |
| Descripción | Integra la API de Mercado Pago para efectuar el cobro con tarjeta o dinero en cuenta de manera segura[cite: 31]. |
| Actores | Principal: Cliente Registrado / Secundario: Mercado Pago[cite: 30, 31] |
| Precondiciones | Existencia de una orden de compra generada en estado "Pendiente"[cite: 31]. |
| Postcondiciones | Éxito: La transacción se valida y retorna token de pago aprobado[cite: 31]. / Fallo: Se registra el motivo del rechazo[cite: 31]. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente ingresa los datos de su tarjeta o selecciona saldo disponible en Mercado Pago[cite: 31]. | La pasarela procesa los datos cifrados mediante protocolo seguro[cite: 31]. |
| 2 | La pasarela emite la respuesta de operación autorizada[cite: 31]. | El sistema recibe el webhook de confirmación e impacta el pago en la base de datos[cite: 31]. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Fondos insuficientes o tarjeta rechazada | La pasarela retorna un código de error. El sistema muestra *"Pago rechazado por la entidad emisora"* sin cancelar el pedido[cite: 31]. |
| E2 | Caída o timeout del servicio externo | Si Mercado Pago no responde en 10 segundos, el sistema muestra *"Servicio de pago no disponible temporalmente"* y guarda el intento para posterior reintento[cite: 31]. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Respuesta de integración por API < 3 segundos[cite: 31]. |
| Frecuencia | Alta[cite: 31] |
| Importancia | Alta[cite: 31] |
| Urgencia | Alta[cite: 31] |

---

## CU-08 — Agendar e Instalación Técnica

| Campo | Detalle |
|-------|---------|
| Identificador | CU-08 |
| Nombre | Agendar e Instalación Técnica |
| Descripción | Permite coordinar la visita técnica en el domicilio del cliente para la colocación de aberturas[cite: 31]. |
| Actores | Principal: Cliente Registrado / Secundario: Operador de Depósito[cite: 30, 31] |
| Precondiciones | El pedido debe estar en estado "Pagado" y contener la solicitud de colocación[cite: 31]. |
| Postcondiciones | Éxito: Se genera la orden de instalación en estado "Agendada"[cite: 31]. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente solicita el servicio adicional de colocación al momento de la compra[cite: 31]. | El sistema marca el flag de instalación en la orden de compra[cite: 31]. |
| 2 | El Operador de Depósito revisa los turnos disponibles en la agenda y asigna la fecha técnica[cite: 30, 31]. | El sistema envía una notificación confirmando la fecha y datos del instalador[cite: 31]. |

---

## CU-10 — Emitir Orden de Compra a Proveedor

| Campo | Detalle |
|-------|---------|
| Identificador | CU-10 |
| Nombre | Emitir Orden de Compra a Proveedor |
| Descripción | Permite generar una solicitud de reposición de mercadería hacia los fabricantes de aberturas[cite: 31]. |
| Actores | Principal: Operador de Depósito / Gestor de Ventas[cite: 30, 31] |
| Precondiciones | El proveedor debe estar dado de alta y activo en la base de datos[cite: 31]. |
| Postcondiciones | Éxito: Se genera el documento de Orden de Compra en estado "Pendiente de entrega" y se envía al proveedor[cite: 30, 31]. / Fallo: La orden no se emite[cite: 31]. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El usuario selecciona un proveedor del listado y presiona "Nueva Orden de Compra"[cite: 31]. | El sistema despliega el formulario con los productos asociados a dicho proveedor[cite: 31]. |
| 2 | El usuario especifica las cantidades de aberturas a solicitar y confirma[cite: 31]. | El sistema registra la orden de compra en estado "Pendiente de entrega" y genera el comprobante[cite: 30, 31]. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Producto discontinuado por proveedor | Si se intenta solicitar un producto dado de baja, el sistema notifica *"El artículo X ya no es suministrado por este proveedor"* e impide su inclusión[cite: 31]. |
| E2 | Proveedor inactivo o suspendido | Si la empresa proveedora se halla suspendida comercialmente, el sistema bloquea el formulario e indica *"El proveedor no se encuentra habilitado para recibir pedidos"*[cite: 30, 31]. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Generación y registro del documento < 2 segundos[cite: 31]. |
| Frecuencia | Media (semanal / quincenal)[cite: 31]. |
| Importancia | Media[cite: 31] |
| Urgencia | Media[cite: 31] |