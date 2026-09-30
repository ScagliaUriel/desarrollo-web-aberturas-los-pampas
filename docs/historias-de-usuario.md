# Historias de usuario

---

## HU-01 — Registro e inicio de sesión de usuario

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente minorista o mayorista, quiero registrarme e iniciar sesión con correo y clave, para acceder a mi perfil y guardar mis datos de facturación. |
| Módulo | Autenticación y Clientes |
| Requisitos relacionados | RF-01, RF-02, RF-03 |

### Criterios de aceptación
1. **Dado** que el cliente ingresa un e-mail no registrado y una clave válida, **cuando** hace clic en "Registrarse", **entonces** el sistema crea la cuenta y le envía un correo de bienvenida.
2. **Dado** que el cliente ingresa un e-mail que ya existe, **cuando** presiona "Registrarse", **entonces** el sistema muestra *"El correo electrónico ya se encuentra registrado"*.
3. **Dado** que el usuario ingresa credenciales válidas, **cuando** hace clic en "Iniciar sesión", **entonces** el sistema le otorga acceso y redirige según su rol.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | No requiere de otros módulos desarrollados para funcionar. |
| Negociable | Sí | Los datos obligatorios del perfil pueden ser ajustados. |
| Valiosa | Sí | Aporta valor indispensable para la identificación del usuario. |
| Estimable | Sí | Estimada en 3 Story Points. |
| Pequeña | Sí | Abordable dentro de un solo sprint. |
| Verificable | Sí | Se comprueba probando casos de éxito y credenciales duplicadas/inválidas. |

---

## HU-02 — Control de acceso por roles y auditoría de acciones

| Campo | Detalle |
|-------|---------|
| Historia | Como administrador, quiero controlar el acceso a los paneles mediante roles y registrar las acciones críticas, para garantizar la seguridad operativa. |
| Módulo | Usuarios y Seguridad |
| Requisitos relacionados | RF-04, RF-05 |

### Criterios de aceptación
1. **Dado** que un usuario con rol "Vendedor" intenta ingresar a la sección de administración de usuarios, **cuando** navega a la URL, **entonces** el sistema deniega el acceso y muestra *"No posee permisos para acceder a esta sección"*.
2. **Dado** que un usuario modifica el precio o stock de un producto, **cuando** guarda la operación, **entonces** el sistema genera una entrada en el log de auditoría.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | No | Depende de que existan los módulos de usuarios y productos para auditar. |
| Negociable | Sí | La lista de acciones a auditar es parametrizable. |
| Valiosa | Sí | Imparable para el control interno de los propietarios del negocio. |
| Estimable | Sí | Estimada en 5 Story Points. |
| Pequeña | Sí | Se limita al middleware de roles y la tabla de auditoría. |
| Verificable | Sí | Se verifica realizando cambios administrativos y consultando el log. |

---

## HU-03 — Consulta y filtrado de aberturas en el catálogo

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero filtrar las aberturas por material y categoría, para encontrar rápidamente el producto que busco. |
| Módulo | Catálogo y Productos |
| Requisitos relacionados | RF-06, RF-07, RF-08 |

### Criterios de aceptación
1. **Dado** que el cliente aplica los filtros "Ventanas" y "Aluminio", **cuando** los ejecuta, **entonces** el catálogo muestra únicamente los productos que coinciden.
2. **Dado** que una consulta no arroja coincidencia, **cuando** finaliza la búsqueda, **entonces** el sistema muestra *"No se encontraron aberturas que coincidan con la búsqueda"*.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Lee datos de la base sin depender de la lógica de pagos. |
| Negociable | Sí | Se pueden agregar más filtros en el futuro. |
| Valiosa | Sí | Mejora la experiencia de navegación del cliente. |
| Estimable | Sí | Estimada en 3 Story Points. |
| Pequeña | Sí | Consulta con filtros acotada. |
| Verificable | Sí | Se valida aplicando distintas combinaciones de búsqueda. |

---

## HU-04 — Solicitud de cotización de aberturas a medida

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente mayorista o profesional, quiero solicitar el presupuesto de una abertura con dimensiones especiales y adjuntar planos, para obtener una cotización personalizada. |
| Módulo | Cotizaciones a Medida |
| Requisitos relacionados | RF-09 |

### Criterios de aceptación
1. **Dado** que el cliente completa ancho, alto, material, vidrio y adjunta plano, **cuando** presiona "Solicitar cotización", **entonces** el sistema genera el ticket en estado "Pendiente de revisión".
2. **Dado** que el cliente ingresa medidas fuera del rango de fabricación, **cuando** intenta enviar, **entonces** el sistema muestra *"Las dimensiones están fuera del rango estándar de fabricación"*.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Funciona como un canal independiente del e-commerce estándar. |
| Negociable | Sí | Los formatos de archivos adjuntos pueden ampliarse. |
| Valiosa | Sí | Abre el canal comercial clave para constructoras y arquitectos. |
| Estimable | Sí | Estimada en 5 Story Points. |
| Pequeña | No | Requiere formulario, carga de archivos y panel de gestión de cotizaciones. |
| Verificable | Sí | Se comprueba enviando solicitudes con y sin planos adjuntos. |

---

## HU-05 — Pago digital de compras y emisión de comprobante

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero pagar mi pedido mediante Mercado Pago, para confirmar la compra de forma inmediata. |
| Módulo | Ventas y Checkout |
| Requisitos relacionados | RF-10, RF-11, RF-12 |

### Criterios de aceptación
1. **Dado** que el cliente paga con éxito en la pasarela, **cuando** Mercado Pago aprueba la transacción, **entonces** el pedido pasa a "Pagado", se descuenta el stock y se envía el comprobante.
2. **Dado** que el pago es denegado, **cuando** la pasarela notifica el rechazo, **entonces** el pedido queda en "Pendiente de pago".

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Se integra como un servicio externo aislado. |
| Negociable | Sí | Las opciones de cobro dependen de las habilitadas en la API. |
| Valiosa | Sí | Es el flujo central para monetizar la plataforma online. |
| Estimable | Sí | Estimada en 8 Story Points. |
| Pequeña | Sí | Limitada al flujo de checkout e integración Webhook. |
| Verificable | Sí | Se valida utilizando las credenciales de prueba en entorno Sandbox. |

---

## HU-06 — Seguimiento del estado logístico del pedido

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero consultar el estado de mi pedido desde mi panel, para conocer cuándo recibiré o podré retirar mi compra. |
| Módulo | Ventas y Logística |
| Requisitos relacionados | RF-13 |

### Criterios de aceptación
1. **Dado** que deposito actualiza el pedido a "Despachado", **cuando** el cliente ingresa a su historial, **entonces** el sistema refleja el nuevo estado.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Es una consulta de lectura sobre las órdenes del cliente. |
| Negociable | Sí | Se pueden sumar notificaciones push en el futuro. |
| Valiosa | Sí | Reduce consultas sobre el estado del envío. |
| Estimable | Sí | Estimada en 2 Story Points. |
| Pequeña | Sí | Es la visualización de un estado dentro de la tabla. |
| Verificable | Sí | Se comprueba modificando el estado desde el panel interno. |