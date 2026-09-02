# Requisitos Funcionales y No Funcionales

Documentación detallada de requisitos para la plataforma web de Aberturas Los Pampas, relevados a partir del diagnóstico operativo, tecnológico y de ciberseguridad.

## 1. Requisitos Funcionales (RF)

### Módulo de Clientes
- **RF-01: Registro de clientes.** El sistema debe permitir el autoregistro de clientes mediante formulario web con validación de datos.
- **RF-02: Inicio de sesión.** El sistema debe permitir a los clientes autenticarse mediante correo electrónico y contraseña.
- **RF-03: Gestión de perfil.** El cliente registrado debe poder visualizar y modificar sus datos personales y direcciones de entrega.

### Módulo de Productos y Catálogo
- **RF-04: Catálogo online.** El sistema debe exhibir el catálogo completo de aberturas (portones, puertas, ventanas, rejas, cortinas) con fotografías, descripciones técnicas y precios.
- **RF-05: Búsqueda y filtrado.** El sistema debe permitir buscar productos por nombre, material (chapa, madera, aluminio) o categoría.
- **RF-06: Visualización de stock.** El sistema debe mostrar la disponibilidad en tiempo real de cada producto en la tienda online.

### Módulo de Ventas y Checkout
- **RF-07: Carrito de compras.** El sistema debe permitir a los clientes seleccionar productos, ajustar cantidades y consolidar un pedido.
- **RF-08: Procesamiento de pagos.** El sistema debe integrarse con la API de Mercado Pago para procesar cobros con tarjetas y medios digitales.
- **RF-09: Generación de comprobantes.** El sistema debe emitir y enviar automáticamente al cliente la confirmación y comprobante de compra por correo electrónico.
- **RF-10: Historial de compras.** El cliente debe poder consultar el listado y detalle de todas sus compras realizadas históricamente.
- **RF-21: Gestión de estado de pedidos.** El sistema debe permitir registrar y consultar el estado logístico de los pedidos (Pendiente, En preparación, Entregado).

### Módulo de Stock e Inventario
- **RF-11: Alta de productos.** El administrador debe poder dar de alta nuevos artículos en el catálogo.
- **RF-12: Modificación de productos.** El administrador debe poder editar precios, descripciones y especificaciones de artículos existentes.
- **RF-13: Baja de productos.** El administrador debe poder discontinuar u ocultar productos del catálogo.
- **RF-14: Actualización automática de stock.** Cada venta concretada debe descontar automáticamente las unidades correspondientes del inventario.
- **RF-15: Alertas de stock mínimo.** El sistema debe emitir notificaciones cuando un producto alcance el umbral mínimo de existencias configurado.

### Módulo de Proveedores
- **RF-16: Registro de proveedores.** El sistema debe permitir administrar la información de contacto, CUIT y facturación de proveedores.
- **RF-17 / RF-22: Generación de órdenes de compra.** El sistema debe permitir emitir y administrar órdenes de compra formalizadas hacia los proveedores.
- **RF-18: Historial de compras a proveedores.** El sistema debe almacenar el registro de todas las adquisiciones realizadas a distribuidores.

### Módulo de Administración y Seguridad
- **RF-19: Gestión de roles y permisos.** El sistema debe controlar el acceso según roles definidos (Administrador, Ventas, Depósito, Cliente).
- **RF-20: Auditoría y registro de actividad.** El sistema debe guardar un log de acciones críticas realizadas por los usuarios internos.

---

## 2. Requisitos No Funcionales (RNF)

### Seguridad
- **RNF-01:** Las contraseñas de los usuarios deben almacenarse mediante algoritmos de encriptación hash seguros.
- **RNF-02:** El sistema debe exigir contraseñas con un nivel mínimo de complejidad (al menos 8 caracteres).
- **RNF-03:** Todo el tráfico entre el navegador y el servidor debe estar cifrado mediante protocolo HTTPS.
- **RNF-04:** El panel de administración debe requerir autenticación obligatoria y sesión con tiempo de expiración.

### Rendimiento y Disponibilidad
- **RNF-05:** El tiempo de respuesta de las consultas al catálogo no debe superar los 3 segundos.
- **RNF-06:** La actualización de stock tras una venta debe ejecutarse en tiempo real.
- **RNF-07:** La plataforma web debe garantizar una disponibilidad (uptime) del 99%.
- **RNF-08:** Se deben programar copias de seguridad (backups) automáticas diarias de la base de datos.

### Usabilidad y Mantenibilidad
- **RNF-09:** La interfaz de usuario debe ser intuitiva, priorizando la facilidad de uso para personal sin capacitación técnica.
- **RNF-10:** El diseño debe ser responsive, adaptándose a dispositivos móviles, tablets y computadoras de escritorio.
- **RNF-11:** La arquitectura del sistema debe permitir actualizaciones de código sin interrumpir la operación del servicio.
- **RNF-12:** El código fuente debe estar adecuadamente estructurado y documentado.

### Escalabilidad y Normativa
- **RNF-13:** La base de datos debe estar optimizada para soportar el crecimiento del catálogo hasta 2.000 productos sin degradas el rendimiento.
- **RNF-14:** El tratamiento de datos debe cumplir con la Ley 25.326 de Protección de Datos Personales de la República Argentina.
- **RNF-15:** Los datos personales de los clientes deben mantenerse bajo estricta confidencialidad.
- **RNF-16:** Se debe garantizar la integridad referencial en la base de datos para evitar registros huérfanos.