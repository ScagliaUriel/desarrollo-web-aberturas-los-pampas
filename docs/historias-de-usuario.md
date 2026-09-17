# Historias de usuario

_Presentar al menos una historia de usuario representativa por módulo._
_Cada historia debe incluir formato clásico, criterios de aceptación y validación INVEST._

---

## HU-01 — Registro e inicio de sesión de usuario

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente minorista o mayorista, quiero registrarme e iniciar sesión con e-mail y contraseña, para acceder a mi perfil, guardar direcciones y consultar mi historial. |
| Módulo | Autenticación y Clientes |
| Requisitos relacionados | RF-01, RF-02, RF-03 |

### Criterios de aceptación

1. **Dado** que el cliente ingresa un e-mail no registrado y clave de 8+ caracteres, **cuando** presiona "Registrarse", **entonces** el sistema crea la cuenta y redirige a su perfil.
2. **Dado** que el cliente ingresa un e-mail ya existente, **cuando** envía el formulario, **entonces** el sistema bloquea el registro e indica *"El e-mail ya se encuentra registrado"*.
3. **Dado** que un usuario ingresa credenciales válidas, **cuando** hace clic en "Iniciar sesión", **entonces** el sistema otorga acceso según su rol (Cliente o Administrador).

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Se puede implementar sin depender del checkout ni del catálogo. |
| Negociable | Sí | Los campos del formulario de registro se pueden ajustar según necesidad. |
| Valiosa | Sí | Permite identificar al cliente y asociar sus compras. |
| Estimable | Sí | Complejidad técnica baja, estimada en 3 Story Points. |
| Pequeña | Sí | Se desarrolla dentro de un solo sprint. |
| Verificable | Sí | Se valida mediante pruebas de autenticación de usuarios. |

---

## HU-02 — Consulta y filtrado de aberturas en el catálogo

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero filtrar el catálogo online por material y categoría, para encontrar rápidamente el producto adecuado para mi obra. |
| Módulo | Catálogo y Productos |
| Requisitos relacionados | RF-04, RF-05, RF-06 |

### Criterios de aceptación

1. **Dado** que el cliente navega por la tienda, **cuando** aplica los filtros "Ventanas" y "Aluminio", **entonces** el catálogo exhibe solo los productos que cumplen ambos criterios.
2. **Dado** que el cliente busca una combinación sin existencias, **cuando** ejecuta la búsqueda, **entonces** el sistema muestra *"No se encontraron aberturas que coincidan con la búsqueda"*.
3. **Dado** que un producto no posee stock disponible, **cuando** se muestra en la grilla, **entonces** exhibe la etiqueta *"Sin stock"* y deshabilita la compra.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Depende de la base de datos de productos pero no de otros módulos. |
| Negociable | Sí | Los filtros se pueden ampliar a medidas o marcas. |
| Valiosa | Sí | Mejora la experiencia de búsqueda y la conversión de ventas. |
| Estimable | Sí | Estimada en 3 Story Points. |
| Pequeña | Sí | Lógica de lectura y filtrado acotada. |
| Verificable | Sí | Se comprueba aplicando combinaciones de filtros en la interfaz. |

---

## HU-03 — Cotización de aberturas a medida

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente o profesional de la construcción, quiero solicitar el presupuesto de una abertura con dimensiones personalizadas, para obtener un costo exacto para productos fuera de catálogo. |
| Módulo | Cotizaciones a Medida |
| Requisitos relacionados | RF-23 |

### Criterios de aceptación

1. **Dado** que el cliente completa alto, ancho, material y tipo de vidrio, **cuando** confirma la solicitud, **entonces** el sistema genera una solicitud de cotización N° X y notifica al área de ventas.
2. **Dado** que el cliente ingresa dimensiones menores al límite de producción (ej. menor a 0.50m), **cuando** intenta enviar, **entonces** el sistema muestra *"Las dimensiones están fuera del rango estándar de fabricación"*.
3. **Dado** que las dimensiones son válidas pero no se adjunta plano, **cuando** envía la solicitud, **entonces** el sistema procesa el pedido marcándolo como "Pendiente de revisión técnica".

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Es autónoma del proceso de compra de productos en stock. |
| Negociable | Sí | Los campos obligatorios de la cotización son adaptables. |
| Valiosa | Sí | Resuelve una necesidad central identificada en el relevamiento comercial. |
| Estimable | Sí | Estimada en 5 Story Points. |
| Pequeña | Sí | Alcance limitado al envío del formulario y registro del ticket. |
| Verificable | Sí | Se prueba enviando datos válidos e inválidos desde la interfaz. |

---

## HU-04 — Pago de pedidos con pasarela digital

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero pagar mi pedido mediante Mercado Pago, para abonar de forma digital y confirmar mi compra inmediatamente. |
| Módulo | Ventas y Checkout |
| Requisitos relacionados | RF-07, RF-08, RF-09 |

### Criterios de aceptación

1. **Dado** que el cliente finaliza el carrito y selecciona Mercado Pago, **cuando** la pasarela aprueba la transacción, **entonces** el pedido pasa a estado "Pagado" y se descuenta el stock.
2. **Dado** que la tarjeta es rechazada o no posee saldo, **cuando** la pasarela notifica el error, **entonces** el pedido queda en "Pendiente de pago" y permite reintentar sin borrar la orden.
3. **Dado** que el pago es aprobado, **cuando** la pasarela confirma el cobro, **entonces** el sistema emite el comprobante y lo envía por e-mail al cliente.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Se conecta mediante API con la pasarela de cobros. |
| Negociable | Sí | Los medios de pago aceptados los gestiona la pasarela. |
| Valiosa | Sí | Es la funcionalidad principal de cobranza para la tienda e-commerce. |
| Estimable | Sí | Estimada en 8 Story Points. |
| Pequeña | Sí | Se limita a la integración e interpretación del checkout. |
| Verificable | Sí | Se valida utilizando las credenciales de prueba en entorno Sandbox. |

---

## HU-05 — Control e inventario automático de stock

| Campo | Detalle |
|-------|---------|
| Historia | Como encargado de depósito, quiero que el inventario se descuente automáticamente con cada compra web, para mantener las existencias reales sincronizadas. |
| Módulo | Depósito y Stock |
| Requisitos relacionados | RF-14, RF-15 |

### Criterios de aceptación

1. **Dado** que una compra por 2 unidades de un portón es aprobada, **cuando** el sistema procesa el pago, **entonces** descuenta 2 unidades del inventario en tiempo real.
2. **Dado** que una venta deja un producto por debajo del umbral mínimo de seguridad, **cuando** se actualiza el stock, **entonces** el sistema emite una alerta de reposición.
3. **Dado** que se cancela un pedido no abonado, **cuando** se vence el plazo de reserva, **entonces** el sistema restituye las unidades al inventario.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Es un evento que responde a la confirmación de la venta. |
| Negociable | Sí | El umbral de stock mínimo se puede parametrizar por producto. |
| Valiosa | Sí | Evita la sobreventa y los quiebres de stock físicos. |
| Estimable | Sí | Estimada en 3 Story Points. |
| Pequeña | Sí | Actualización directa en la capa de datos. |
| Verificable | Sí | Se verifica comparando el stock antes y después de una orden. |

---

## HU-06 — Gestión de órdenes de compra a proveedores

| Campo | Detalle |
|-------|---------|
| Historia | Como administrador, quiero emitir y consultar órdenes de compra dirigidas a proveedores, para gestionar el reabastecimiento de aberturas de forma organizada. |
| Módulo | Proveedores |
| Requisitos relacionados | RF-16, RF-17, RF-18 |

### Criterios de aceptación

1. **Dado** que el administrador selecciona un proveedor y los ítems requeridos, **cuando** genera la orden, **entonces** el sistema emite el documento en estado "Pendiente de entrega".
2. **Dado** que un proveedor se encuentra inactivo, **cuando** se redacta una nueva orden, **entonces** el sistema no lo despliega en la lista de proveedores seleccionables.
3. **Dado** que se registra la recepción de la mercadería, **cuando** el encargado de depósito confirma el remito, **entonces** la orden cambia a "Completada" y se incrementa el stock.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Módulo administrativo aislado del e-commerce público. |
| Negociable | Sí | La estructura del documento impreso o digital se puede adaptar. |
| Valiosa | Sí | Formaliza la relación y pedidos de reabastecimiento con los fabricantes. |
| Estimable | Sí | Estimada en 5 Story Points. |
| Pequeña | Sí | Es una gestión CRUD con generación de comprobantes. |
| Verificable | Sí | Se comprueba emitiendo y listando órdenes de compra en el panel. |