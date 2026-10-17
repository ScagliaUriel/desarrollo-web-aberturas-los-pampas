# Casos de uso

El código PlantUML del diagrama general está en [`diagramas/casos-de-uso.puml`](../diagramas/casos-de-uso.puml). Cada caso de uso se corresponde con una pantalla de los wireframes de [`diagramas/wireframes`](../diagramas/wireframes).

## Actores

- **Cliente:** visitante sin sesión. Consulta el catálogo e inicia sesión o se registra.
- **Cliente Registrado:** hereda del Cliente. Cotiza a medida, arma el carrito, paga y consulta sus pedidos.
- **Gestor de Ventas:** personal interno. Revisa cotizaciones, emite órdenes de compra y consulta el dashboard.
- **Operador de Depósito:** personal interno. Administra productos y stock, controla despachos y coordina instalaciones.
- **Administrador:** personal interno con máximos privilegios. Controla roles, consulta el registro de auditoría y administra proveedores.
- **Mercado Pago:** sistema externo. Procesa y valida los cobros.

## Trazabilidad con los wireframes

| Caso de uso | Wireframe | Actores |
|---|---|---|
| CU-01 — Consultar Catálogo | wf 01, 02 | Cliente / Cliente Registrado |
| CU-02 — Solicitar Cotización a Medida | wf 11 | Principal: Cliente Registrado / Secundario: Gestor de Ventas |
| CU-03 — Iniciar Sesión / Registrarse | wf 01 "Ingresar", wf 06 | Cliente / Gestor de Ventas / Operador de Depósito |
| CU-04 — Gestionar Carrito | wf 03 | Cliente Registrado |
| CU-05 — Realizar Checkout | wf 04 | Principal: Cliente Registrado |
| CU-06 — Procesar Pago Digital | wf 04 | Principal: Cliente Registrado / Secundario: Mercado Pago |
| CU-07 — Consultar Mis Pedidos y Cotizaciones | wf 05 | Cliente Registrado |
| CU-08 — Gestionar Productos y Stock | wf 07 | Operador de Depósito |
| CU-09 — Controlar Pedidos y Despachos | wf 09 | Operador de Depósito |
| CU-10 — Coordinar Instalación | wf 09 | Operador de Depósito |
| CU-11 — Generar Orden de Compra | wf 08 | Gestor de Ventas / Operador de Depósito |
| CU-12 — Ver Dashboard de Ventas | wf 10 | Gestor de Ventas |
| CU-13 — Consultar Registro de Auditoría | - | Administrador |
| CU-14 — ABM de Proveedores | wf 08 | Administrador |

---

## CU-01 — Consultar Catálogo

| Campo | Detalle |
|---|---|
| Identificador | CU-01 |
| Nombre | Consultar Catálogo |
| Pantalla | wf 01, 02 |
| Descripción | El cliente navega los productos destacados y el detalle de cada abertura (especificaciones, precio y disponibilidad). |
| Actores | Cliente / Cliente Registrado |
| Precondiciones | Ninguna (acceso público). |
| Postcondiciones | Se exhibe el producto con su precio y estado de stock. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente ingresa al sitio o a "Catálogo". | El sistema muestra los productos destacados con imagen, nombre, descripción y precio. |
| 2 | El cliente selecciona un producto. | El sistema muestra la ficha con especificaciones técnicas, precio e indicador "Stock Disponible". |
| 3 | El cliente presiona "Añadir al Carrito" o "Solicitar a Medida". | El sistema ejecuta CU-04 (agrega el producto) o redirige a CU-02 (extend). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Producto sin stock | El sistema muestra "Sin stock" y el plazo de entrega estimado; deshabilita "Añadir al Carrito" y deja disponible "Solicitar a Medida". |

| Campo | Detalle |
|---|---|
| Rendimiento | < 3 segundos en la carga del catálogo. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-02 — Solicitar Cotización a Medida

| Campo | Detalle |
|---|---|
| Identificador | CU-02 |
| Nombre | Solicitar Cotización a Medida |
| Pantalla | wf 11 |
| Descripción | El cliente configura una abertura fuera de catálogo (tipología, dimensiones, vidrio, color, observaciones y plano técnico opcional), obtiene una estimación y la envía a revisión técnica. |
| Actores | Principal: Cliente Registrado / Secundario: Gestor de Ventas |
| Precondiciones | El cliente puede ingresar a la cotización desde el catálogo y, si no tiene sesión iniciada, el sistema deriva a CU-03 para autenticarse antes de enviar la solicitud. Se invoca como extensión de CU-01 desde "Solicitar a Medida" o "Cotizar a Medida". |
| Postcondiciones | Éxito: se registra la solicitud en estado "En Revisión" con `url_plano` cuando fue adjuntado y queda visible en Mis Pedidos (CU-07). Fallo: no se registra. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente selecciona la tipología e ingresa ancho y alto en mm. | El sistema valida que las dimensiones estén dentro del rango de fabricación. |
| 2 | El cliente elige tipo de vidrio, color/acabado, completa observaciones y, si corresponde, adjunta el plano técnico en `url_plano`. | El sistema guarda la configuración y conserva la referencia del plano cuando se carga. |
| 3 | El cliente presiona "Calcular Estimación". | El sistema muestra el resumen: materiales, mano de obra, vidrio y total estimado. |
| 4 | El cliente presiona "Enviar a Revisión Técnica". | El sistema registra la solicitud N° COT-X en estado "En Revisión" con la información completa y notifica al Gestor de Ventas. |
| 5 | El Gestor de Ventas revisa la solicitud. | El sistema actualiza su estado y notifica al cliente. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Dimensiones fuera de rango (menor a 500 mm o mayor a 3000 mm) | El sistema muestra "Las dimensiones están fuera del rango estándar de fabricación" y no calcula la estimación. |
| E2 | Cliente sin sesión iniciada | Al presionar "Enviar a Revisión Técnica" el sistema deriva a CU-03 y, al ingresar, retoma la cotización. |

| Campo | Detalle |
|---|---|
| Rendimiento | Cálculo de estimación < 2 segundos. |
| Frecuencia | Media |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-03 — Iniciar Sesión / Registrarse

| Campo | Detalle |
|---|---|
| Identificador | CU-03 |
| Nombre | Iniciar Sesión / Registrarse |
| Pantalla | wf 01 "Ingresar", wf 06 |
| Descripción | Autenticación de clientes y del personal interno, y alta de cuenta para clientes nuevos. |
| Actores | Cliente / Gestor de Ventas / Operador de Depósito |
| Precondiciones | El usuario no tiene sesión activa. |
| Postcondiciones | Éxito: sesión iniciada con los permisos de su rol. Fallo: acceso denegado. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El usuario ingresa correo y contraseña. | El sistema valida las credenciales. |
| 2 | El sistema identifica el rol asignado al usuario. | El sistema redirige al sitio (cliente) o al panel interno (personal). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Credenciales inválidas | El sistema informa "Usuario o contraseña incorrectos". |
| E2 | Correo ya registrado (alta de cliente) | El sistema informa "El e-mail ya se encuentra registrado" y no crea la cuenta. |
| E3 | Sesión del panel inactiva 15 minutos | El sistema cierra la sesión del personal interno. |

| Campo | Detalle |
|---|---|
| Rendimiento | Respuesta < 2 segundos. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-04 — Gestionar Carrito

| Campo | Detalle |
|---|---|
| Identificador | CU-04 |
| Nombre | Gestionar Carrito |
| Pantalla | wf 03 |
| Descripción | El cliente revisa los productos agregados, ajusta cantidades y decide si solicita instalación. |
| Actores | Cliente Registrado |
| Precondiciones | El cliente tiene al menos un producto en el carrito. |
| Postcondiciones | El carrito refleja cantidades, instalación y total actualizados. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente abre "Mi Carrito de Compras". | El sistema lista los productos con cantidad, precio unitario y subtotal. |
| 2 | El cliente modifica la cantidad con − / +. | El sistema recalcula el subtotal y el total. |
| 3 | El cliente tilda "Solicitar servicio de colocación e instalación". | El sistema suma el servicio de instalación al resumen. |
| 4 | El cliente presiona "Proceder al Checkout". | El sistema ejecuta CU-05. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Cantidad mayor al stock | El sistema informa "Solo quedan X unidades disponibles" y mantiene la cantidad máxima. |
| E2 | Carrito vacío | El sistema muestra "Tu carrito está vacío" y oculta el botón de checkout. |

| Campo | Detalle |
|---|---|
| Rendimiento | Recálculo inmediato. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-05 — Realizar Checkout

| Campo | Detalle |
|---|---|
| Identificador | CU-05 |
| Nombre | Realizar Checkout |
| Pantalla | wf 04 |
| Descripción | El cliente confirma datos de facturación, dirección de entrega o instalación y método de pago. |
| Actores | Principal: Cliente Registrado |
| Precondiciones | El cliente está autenticado y tiene productos en el carrito. |
| Postcondiciones | Éxito: pedido generado y pago procesado (CU-06). Fallo: pedido "Pendiente de pago" con stock intacto. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente revisa datos personales y de facturación. | El sistema muestra los datos del cliente precargados. |
| 2 | El cliente confirma la dirección de entrega o instalación. | El sistema valida la dirección. |
| 3 | El cliente elige el método de pago y presiona "Pagar con Mercado Pago" (si elige transferencia bancaria, ver E3). | El sistema ejecuta CU-06 (include). |
| 4 | El cliente visualiza el resultado. | El sistema muestra la confirmación y envía el comprobante por e-mail. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Falta de stock al confirmar | El sistema bloquea el checkout, informa "Producto sin stock disponible" y devuelve al carrito. |
| E2 | Pago rechazado | El pedido queda "Pendiente de pago" y se ofrece reintentar. |
| E3 | El cliente elige transferencia bancaria en el paso 3 | El sistema no ejecuta CU-06, muestra los datos de la transferencia (CBU / Alias) y registra el pedido como "Pendiente de pago" hasta que el personal de ventas confirme la acreditación. |

| Campo | Detalle |
|---|---|
| Rendimiento | Carga de pantalla < 2 segundos. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-06 — Procesar Pago Digital

| Campo | Detalle |
|---|---|
| Identificador | CU-06 |
| Nombre | Procesar Pago Digital |
| Pantalla | wf 04 |
| Descripción | El sistema delega el cobro en Mercado Pago (tarjetas, débito o dinero en cuenta). |
| Actores | Principal: Cliente Registrado / Secundario: Mercado Pago |
| Precondiciones | Existe un pedido generado en estado "Pendiente de pago". |
| Postcondiciones | Éxito: pago aprobado y stock descontado. Fallo: se registra el motivo del rechazo. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente ingresa los datos de pago en la pasarela. | Mercado Pago procesa los datos cifrados. |
| 2 | Mercado Pago informa el resultado. | El sistema recibe el webhook, marca el pedido "Pagado" y descuenta el stock. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Fondos insuficientes o tarjeta rechazada | El sistema muestra "Pago rechazado por la entidad emisora" sin cancelar el pedido. |
| E2 | Timeout de Mercado Pago (10 s) | El sistema muestra "Servicio de pago no disponible temporalmente" y guarda el intento para reintento. |

| Campo | Detalle |
|---|---|
| Rendimiento | Respuesta de integración < 3 segundos. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-07 — Consultar Mis Pedidos y Cotizaciones

| Campo | Detalle |
|---|---|
| Identificador | CU-07 |
| Nombre | Consultar Mis Pedidos y Cotizaciones |
| Pantalla | wf 05 |
| Descripción | El cliente consulta su historial de pedidos y solicitudes de cotización con estado de pago y logística. |
| Actores | Cliente Registrado |
| Precondiciones | El cliente está autenticado. |
| Postcondiciones | Se muestra el historial con el estado actual de cada pedido y cotización. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El cliente ingresa a "Mis Pedidos". | El sistema muestra sus datos y el historial (N° de pedido, fecha, estado de pago, logística y total). |
| 2 | El cliente revisa una cotización. | El sistema muestra su estado ("En Revisión") y el total como "Pendiente" hasta que Ventas la cotiza. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Cliente sin pedidos | El sistema informa "Todavía no realizaste pedidos". |

| Campo | Detalle |
|---|---|
| Rendimiento | < 2 segundos. |
| Frecuencia | Media |
| Importancia | Media |
| Urgencia | Media |

---

## CU-08 — Gestionar Productos y Stock

| Campo | Detalle |
|---|---|
| Identificador | CU-08 |
| Nombre | Gestionar Productos y Stock |
| Pantalla | wf 07 |
| Descripción | ABM de productos y control del stock, con alerta visual de stock mínimo. |
| Actores | Operador de Depósito |
| Precondiciones | Usuario del personal autenticado con rol habilitado. |
| Postcondiciones | El catálogo y el stock quedan actualizados. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El operador ingresa a "Gestión de Inventario y Stock". | El sistema lista ID, producto, categoría, precio base, stock actual y estado. |
| 2 | El operador busca por nombre o ID, o filtra por línea. | El sistema recalcula el listado. |
| 3 | El operador presiona "+ Nuevo Producto" o edita uno existente. | El sistema muestra el formulario del producto. |
| 4 | El operador guarda los cambios. | El sistema valida, persiste y registra el movimiento de stock. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Producto con stock en el mínimo | El sistema marca el estado "Stock Mínimo" y lo suma a las alertas del dashboard (CU-12). |
| E2 | Ajuste que deja stock negativo | El sistema rechaza la operación. |
| E3 | Baja de producto con pedidos pendientes | El sistema bloquea la baja y sugiere discontinuarlo. |

| Campo | Detalle |
|---|---|
| Rendimiento | < 2 segundos por operación. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Media |

---

## CU-09 — Controlar Pedidos y Despachos

| Campo | Detalle |
|---|---|
| Identificador | CU-09 |
| Nombre | Controlar Pedidos y Despachos |
| Pantalla | wf 09 |
| Descripción | El operador revisa los pedidos y avanza su estado logístico. |
| Actores | Operador de Depósito |
| Precondiciones | Existen pedidos registrados. |
| Postcondiciones | El estado logístico del pedido queda actualizado y el cliente lo ve en CU-07. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El operador ingresa a "Control de Pedidos y Despachos". | El sistema lista ID, cliente, fecha, estado de pago, logística e instalación. |
| 2 | El operador selecciona un pedido pagado y avanza su estado. | El sistema lo pasa de "En preparación" a "Entregado" y notifica al cliente por e-mail. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Pedido con pago pendiente | El sistema no permite avanzar su estado logístico y lo mantiene "En espera". |
| E2 | Pedido ya entregado | El sistema no admite nuevos cambios de estado. |

| Campo | Detalle |
|---|---|
| Rendimiento | < 2 segundos. |
| Frecuencia | Alta |
| Importancia | Alta |
| Urgencia | Alta |

---

## CU-10 — Coordinar Instalación

| Campo | Detalle |
|---|---|
| Identificador | CU-10 |
| Nombre | Coordinar Instalación |
| Pantalla | wf 09 |
| Descripción | El operador agenda la instalación en obra de los pedidos que la solicitaron en el carrito. |
| Actores | Operador de Depósito |
| Precondiciones | El pedido está pagado y el cliente solicitó instalación. Extiende CU-09. |
| Postcondiciones | La instalación queda en estado "Agendada" con fecha programada. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El operador selecciona un pedido con instalación pendiente. | El sistema muestra la dirección de obra y los productos a instalar. |
| 2 | El operador indica la fecha de instalación y confirma. | El sistema registra "Sí (Agendada)" y notifica al cliente. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Pedido que no solicitó instalación | El sistema no habilita la acción "Agendar". |
| E2 | Fecha anterior a hoy | El sistema informa "La fecha debe ser posterior a la actual". |

| Campo | Detalle |
|---|---|
| Rendimiento | < 2 segundos. |
| Frecuencia | Media |
| Importancia | Media |
| Urgencia | Media |

---

## CU-11 — Generar Orden de Compra

| Campo | Detalle |
|---|---|
| Identificador | CU-11 |
| Nombre | Generar Orden de Compra |
| Pantalla | wf 08 |
| Descripción | Emisión de una orden de reabastecimiento a un proveedor, con detalle de materiales, cantidades y costo. |
| Actores | Gestor de Ventas / Operador de Depósito |
| Precondiciones | El proveedor está dado de alta y activo. |
| Postcondiciones | Éxito: orden generada en estado "Pendiente de entrega" y exportada a PDF. Fallo: no se emite. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El usuario selecciona un proveedor. | El sistema muestra los materiales asociados (código, descripción, cantidad, costo unitario). |
| 2 | El usuario define las cantidades a solicitar. | El sistema calcula el total estimado. |
| 3 | El usuario presiona "Generar Orden de Compra (PDF)". | El sistema registra la orden N° X y genera el PDF. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Material discontinuado por el proveedor | El sistema informa "El artículo X ya no es suministrado por este proveedor" e impide incluirlo. |
| E2 | Proveedor inactivo | El sistema no lo despliega entre los proveedores seleccionables. |

| Campo | Detalle |
|---|---|
| Rendimiento | Generación del documento < 2 segundos. |
| Frecuencia | Media (semanal / quincenal) |
| Importancia | Media |
| Urgencia | Media |

---

## CU-12 — Ver Dashboard de Ventas

| Campo | Detalle |
|---|---|
| Identificador | CU-12 |
| Nombre | Ver Dashboard de Ventas |
| Pantalla | wf 10 |
| Descripción | Visualización de indicadores del mes para apoyar decisiones de venta y reposición. |
| Actores | Gestor de Ventas |
| Precondiciones | Usuario del personal autenticado con rol habilitado. |
| Postcondiciones | Se muestran los indicadores del período. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El gestor ingresa a "Dashboard y Métrica de Ventas". | El sistema muestra ventas del mes, pedidos procesados, cotizaciones aprobadas y alertas de stock mínimo. |
| 2 | El gestor revisa la evolución y la distribución por material. | El sistema muestra la evolución mensual y las ventas por material. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Sin ventas en el período | El sistema muestra los indicadores en cero y un mensaje informativo. |

| Campo | Detalle |
|---|---|
| Rendimiento | Cálculo del dashboard < 3 segundos. |
| Frecuencia | Media |
| Importancia | Media |
| Urgencia | Baja |

---

## CU-13 — Consultar Registro de Auditoría

|| Campo | Detalle |
|---|---|
| Identificador | CU-13 |
| Nombre | Consultar Registro de Auditoría |
| Pantalla | - |
| Descripción | El administrador consulta el historial de acciones críticas del sistema (modificaciones de precios, cambios manuales de stock y anulaciones de pedidos) con referencia al registro afectado, usuario, fecha y valores anteriores/nuevos. |
| Actores | Administrador |
| Precondiciones | Usuario autenticado con rol de Administrador. |
| Postcondiciones | Se muestra el registro de auditoría filtrado según los criterios seleccionados. |

### Secuencia normal

|| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El administrador ingresa a "Registro de Auditoría". | El sistema lista las entradas con fecha, acción, tabla afectada, registro afectado, usuario, valor anterior y valor nuevo. |
| 2 | El administrador filtra por rango de fechas, acción o usuario. | El sistema recalcula el listado según los filtros aplicados. |

### Excepciones

|| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Sin registros en el período filtrado | El sistema muestra un mensaje informativo *"No se encontraron registros de auditoría en el período seleccionado"*. |

|| Campo | Detalle |
|---|---|
| Rendimiento | Consulta < 2 segundos. |
| Frecuencia | Baja |
| Importancia | Alta |
| Urgencia | Baja |

---

## CU-14 — ABM de Proveedores

|| Campo | Detalle |
|---|---|
| Identificador | CU-14 |
| Nombre | ABM de Proveedores |
| Pantalla | wf 08 |
| Descripción | El administrador administra los datos de contacto y rubro de los proveedores: alta, baja y modificación de registros. |
| Actores | Administrador |
| Precondiciones | Usuario autenticado con rol de Administrador. |
| Postcondiciones | El catálogo de proveedores queda actualizado. |

### Secuencia normal

|| # | Acción (actor) | Reacción (sistema) |
|---|---|---|
| 1 | El administrador ingresa a "Gestión de Proveedores". | El sistema lista razón social, teléfono, e-mail y estado de los proveedores. |
| 2 | El administrador presiona "+ Nuevo Proveedor" o edita uno existente. | El sistema muestra el formulario del proveedor. |
| 3 | El administrador completa o modifica razón social, teléfono, e-mail y rubro. | El sistema valida, persiste y registra el movimiento. |

### Excepciones

|| # | Situación | Respuesta del sistema |
|---|---|---|
| E1 | Proveedor con órdenes de compra activas | El sistema bloquea la baja y sugiere discontinuarlo. |
| E2 | E-mail duplicado | El sistema informa *"El e-mail ya se encuentra registrado para otro proveedor"*. |

|| Campo | Detalle |
|---|---|
| Rendimiento | Operación < 2 segundos. |
| Frecuencia | Baja |
| Importancia | Media |
| Urgencia | Baja |

---
