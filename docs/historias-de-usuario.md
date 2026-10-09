# Historias de usuario

---

## HU-01 — Registro e inicio de sesión de usuario

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente minorista o mayorista, quiero registrarme e iniciar sesión con correo y clave, para acceder a mi perfil y guardar mis datos de facturación[cite: 31]. |
| Módulo | Autenticación y Clientes[cite: 31] |
| Requisitos relacionados | RF-01, RF-02, RF-03[cite: 31] |

### Criterios de aceptación
1. **Dado** que el cliente ingresa un e-mail no registrado y una clave válida, **cuando** hace clic en "Registrarse", **entonces** el sistema crea la cuenta y le envía un correo de bienvenida[cite: 31].
2. **Dado** que el cliente ingresa un e-mail que ya existe, **cuando** presiona "Registrarse", **entonces** el sistema muestra *"El correo electrónico ya se encuentra registrado"*[cite: 31].
3. **Dado** que el usuario ingresa credenciales válidas, **cuando** hace clic en "Iniciar sesión", **entonces** el sistema le otorga acceso y redirige según su rol[cite: 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | No requiere de otros módulos desarrollados para funcionar[cite: 31]. |
| Negociable | Sí | Los datos obligatorios del perfil pueden ser ajustados[cite: 31]. |
| Valiosa | Sí | Aporta valor indispensable para la identificación del usuario[cite: 31]. |
| Estimable | Sí | Estimada en 3 Story Points[cite: 31]. |
| Pequeña | Sí | Abordable dentro de un solo sprint[cite: 31]. |
| Verificable | Sí | Se comprueba probando casos de éxito y credenciales duplicadas/inválidas[cite: 31]. |

---

## HU-02 — Control de acceso por roles y auditoría de acciones

| Campo | Detalle |
|-------|---------|
| Historia | Como administrador, quiero controlar el acceso a los paneles mediante roles y registrar las acciones críticas, para garantizar la seguridad operativa[cite: 31]. |
| Módulo | Usuarios y Seguridad[cite: 31] |
| Requisitos relacionados | RF-04, RF-05[cite: 31] |

### Criterios de aceptación
1. **Dado** que un usuario con rol "Personal de Ventas" intenta ingresar a la sección de administración de usuarios, **cuando** navega a la URL, **entonces** el sistema deniega el acceso y muestra *"No posee permisos para acceder a esta sección"*[cite: 31].
2. **Dado** que un usuario modifica el precio o stock de un producto, **cuando** guarda la operación, **entonces** el sistema genera una entrada en el log de auditoría[cite: 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | No | Depende de que existan los módulos de usuarios y productos para auditar[cite: 30, 31]. |
| Negociable | Sí | La lista de acciones a auditar es parametrizable[cite: 31]. |
| Valiosa | Sí | Imprescindible para el control interno de los propietarios del negocio[cite: 30, 31]. |
| Estimable | Sí | Estimada en 5 Story Points[cite: 31]. |
| Pequeña | Sí | Se limita al middleware de roles y la tabla de auditoría[cite: 31]. |
| Verificable | Sí | Se verifica realizando cambios administrativos y consultando el log[cite: 31]. |

---

## HU-03 — Consulta y filtrado de aberturas en el catálogo

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero filtrar las aberturas por material y categoría, para encontrar rápidamente el producto que busco[cite: 31]. |
| Módulo | Catálogo y Productos[cite: 31] |
| Requisitos relacionados | RF-06, RF-07, RF-08[cite: 31] |

### Criterios de aceptación
1. **Dado** que el cliente aplica los filtros "Ventanas" y "Aluminio", **cuando** los ejecuta, **entonces** el catálogo muestra únicamente los productos que coinciden[cite: 31].
2. **Dado** que una consulta no arroja coincidencia, **cuando** finaliza la búsqueda, **entonces** el sistema muestra *"No se encontraron aberturas que coincidan con la búsqueda"*[cite: 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Lee datos de la base sin depender de la lógica de pagos[cite: 31]. |
| Negociable | Sí | Se pueden agregar más filtros en el futuro[cite: 31]. |
| Valiosa | Sí | Mejora la experiencia de navegación del cliente[cite: 31]. |
| Estimable | Sí | Estimada en 3 Story Points[cite: 31]. |
| Pequeña | Sí | Consulta con filtros acotada[cite: 31]. |
| Verificable | Sí | Se valida aplicando distintas combinaciones de búsqueda[cite: 31]. |

---

## HU-04 — Solicitud de cotización de aberturas a medida

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente mayorista o profesional, quiero solicitar el presupuesto de una abertura con dimensiones especiales y adjuntar planos, para obtener una cotización personalizada[cite: 31]. |
| Módulo | Cotizaciones a Medida[cite: 31] |
| Requisitos relacionados | RF-09[cite: 31] |

### Criterios de aceptación
1. **Dado** que el cliente completa ancho, alto, material, vidrio y adjunta plano, **cuando** presiona "Solicitar cotización", **entonces** el sistema genera el ticket en estado "Pendiente de revisión"[cite: 31].
2. **Dado** que el cliente ingresa medidas fuera del rango de fabricación, **cuando** intenta enviar, **entonces** el sistema muestra *"Las dimensiones están fuera del rango estándar de fabricación"*[cite: 31].
3. **Dado** que el cliente ingresa medidas válidas sin adjuntar plano, **cuando** presiona "Solicitar cotización", **entonces** el sistema registra la solicitud correctamente en estado "Pendiente de revisión"[cite: 30, 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Funciona como un canal independiente del e-commerce estándar[cite: 31]. |
| Negociable | Sí | Los formatos de archivos adjuntos pueden ampliarse[cite: 31]. |
| Valiosa | Sí | Abre el canal comercial clave para constructoras y arquitectos[cite: 31]. |
| Estimable | Sí | Estimada en 5 Story Points[cite: 31]. |
| Pequeña | No | Requiere formulario, carga de archivos y panel de gestión de cotizaciones[cite: 30, 31]. |
| Verificable | Sí | Se comprueba enviando solicitudes con y sin planos adjuntos[cite: 31]. |

---

## HU-05 — Pago digital de compras y emisión de comprobante

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero pagar mi pedido mediante Mercado Pago, para confirmar la compra de forma inmediata[cite: 31]. |
| Módulo | Ventas y Checkout[cite: 31] |
| Requisitos relacionados | RF-10, RF-11, RF-12[cite: 31] |

### Criterios de aceptación
1. **Dado** que el cliente paga con éxito en la pasarela, **cuando** Mercado Pago aprueba la transacción, **entonces** el pedido pasa a "Pagado", se descuenta el stock y se envía el comprobante[cite: 31].
2. **Dado** que el pago es denegado, **cuando** la pasarela notifica el rechazo, **entonces** el pedido queda en "Pendiente de pago"[cite: 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Se integra como un servicio externo aislado[cite: 31]. |
| Negociable | Sí | Las opciones de cobro dependen de las habilitadas en la API[cite: 31]. |
| Valiosa | Sí | Es el flujo central para monetizar la plataforma online[cite: 31]. |
| Estimable | Sí | Estimada en 8 Story Points[cite: 31]. |
| Pequeña | Sí | Limitada al flujo de checkout e integración Webhook[cite: 31]. |
| Verificable | Sí | Se valida utilizando las credenciales de prueba en entorno Sandbox[cite: 31]. |

---

## HU-06 — Seguimiento del estado logístico del pedido

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero consultar el estado de mi pedido desde mi panel, para conocer cuándo recibiré o podré retirar mi compra[cite: 31]. |
| Módulo | Ventas y Logística[cite: 31] |
| Requisitos relacionados | RF-13[cite: 31] |

### Criterios de aceptación
1. **Dado** que depósito actualiza el pedido a "Despachado", **cuando** el cliente ingresa a su historial, **entonces** el sistema refleja el nuevo estado[cite: 31].
2. **Dado** que el pedido se encuentra en preparación, **cuando** el cliente selecciona el pedido, **entonces** el sistema muestra la fecha estimada de despacho y el método asignado[cite: 30, 31].

### Excepciones
1. **E1 - Número de pedido inexistente o cancelado:** Si la orden fue anulada por falta de pago, el sistema muestra el mensaje *"El pedido seleccionado se encuentra cancelado"*[cite: 30, 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Es una consulta de lectura sobre las órdenes del cliente[cite: 31]. |
| Negociable | Sí | Se pueden sumar notificaciones push en el futuro[cite: 31]. |
| Valiosa | Sí | Reduce consultas sobre el estado del envío[cite: 31]. |
| Estimable | Sí | Estimada en 2 Story Points[cite: 31]. |
| Pequeña | Sí | Es la visualización de un estado dentro de la tabla[cite: 31]. |
| Verificable | Sí | Se comprueba modificando el estado desde el panel interno[cite: 31]. |

---

## HU-07 — Control de inventario y alertas de stock mínimo

| Campo | Detalle |
|-------|---------|
| Historia | Como operador de depósito, quiero recibir notificaciones cuando las aberturas alcancen el umbral de stock mínimo, para solicitar reposición a los proveedores a tiempo[cite: 30, 31]. |
| Módulo | Stock, Depósito y Proveedores[cite: 30, 31] |
| Requisitos relacionados | RF-15, RF-16[cite: 30, 31] |

### Criterios de aceptación
1. **Dado** que la venta de un producto reduce su stock por debajo del límite mínimo parametrizado, **cuando** se confirma la transacción, **entonces** el sistema emite una alerta visual en el panel de depósito[cite: 30, 31].
2. **Dado** que el operador ingresa al módulo de stock, **cuando** filtra por "Bajo stock", **entonces** el sistema despliega el listado consolidado de artículos a reponer[cite: 30, 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Monitorea la tabla de productos de forma directa[cite: 31]. |
| Negociable | Sí | Los umbrales de alerta se pueden configurar por producto[cite: 31]. |
| Valiosa | Sí | Evita el quiebre de stock y la pérdida de ventas[cite: 31]. |
| Estimable | Sí | Estimada en 3 Story Points[cite: 31]. |
| Pequeña | Sí | Consulta acotada con bandera de alerta[cite: 31]. |
| Verificable | Sí | Se comprueba forzando una venta que reduzca el inventario al mínimo[cite: 31]. |

---

## HU-08 — Generación y emisión de Órdenes de Compra a Proveedores

| Campo | Detalle |
|-------|---------|
| Historia | Como operador de depósito o gestor de ventas, quiero generar una orden de compra hacia un proveedor registrado, para reabastecer el inventario de la fábrica[cite: 30, 31]. |
| Módulo | Stock, Depósito y Proveedores[cite: 30, 31] |
| Requisitos relacionados | RF-17, RF-18[cite: 30, 31] |

### Criterios de aceptación
1. **Dado** que el operador selecciona un proveedor y los artículos con sus cantidades, **cuando** confirma la emisión, **entonces** el sistema genera la Orden de Compra en estado "Pendiente de entrega" y crea el documento PDF[cite: 30, 31].
2. **Dado** que un proveedor se encuentra inactivo, **cuando** el operador intenta asociarle una orden, **entonces** el sistema bloquea la acción y notifica *"El proveedor seleccionado se encuentra inactivo"*[cite: 30, 31].

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Opera de forma aislada entre la entidad Proveedor y OrdenCompra[cite: 31]. |
| Negociable | Sí | Se pueden incorporar firmas digitales o envíos automáticos por correo[cite: 31]. |
| Valiosa | Sí | Formaliza y automatiza el canal de reabastecimiento[cite: 31]. |
| Estimable | Sí | Estimada en 5 Story Points[cite: 31]. |
| Pequeña | Sí | Formulario de emisión con detalle de ítems[cite: 31]. |
| Verificable | Sí | Se verifica emitiendo una orden de compra de prueba y revisando la base de datos[cite: 31]. |