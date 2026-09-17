# Requisitos Funcionales y No Funcionales

Documentación detallada de requisitos para la plataforma web de Aberturas Los Pampas, relevados a partir del diagnóstico operativo, tecnológico y de ciberseguridad.

## 1. Requisitos Funcionales (RF)

### Módulo de Clientes
- **RF-01: Registro de clientes.** El sistema debe permitir el autoregistro de clientes mediante formulario web con validación de datos. *Ejemplo:* Un cliente minorista se registra ingresando su e-mail y DNI para comprar un portón.
- **RF-02: Inicio de sesión.** El sistema debe permitir a los clientes autenticarse mediante correo electrónico y contraseña.
- **RF-03: Gestión de perfil.** El cliente registrado debe poder visualizar y modificar sus datos personales y direcciones de entrega.

### Módulo de Productos y Catálogo
- **RF-04: Catálogo online.** El sistema debe exhibir el catálogo completo de aberturas (portones, puertas, ventanas, rejas, cortinas) con fotografías, descripciones técnicas y precios. *Ejemplo:* Buscar "portones corredizos" o filtrar por "ventanas de aluminio".
- **RF-05: Búsqueda y filtrado.** El sistema debe permitir buscar productos por nombre, material (chapa, madera, aluminio) o categoría.
- **RF-06: Visualización de stock.** El sistema debe mostrar la disponibilidad en tiempo real de cada producto en la tienda online.
- **RF-23: Cotización de aberturas a medida.** El sistema debe permitir al cliente ingresar especificaciones y dimensiones personalizadas (alto, ancho, material, tipo de vidrio) para solicitar el presupuesto de una abertura a medida que no posea stock estándar. *Ejemplo:* Una constructora solicita cotizar una ventana de aluminio de 2.40m x 1.20m con doble vidrio templado.

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
- **RF-17 / RF-22: Generación de órdenes de compra.** El sistema debe permitir emitir y administrar órdenes de compra formalizadas hacia los proveedores. *Ejemplo:* Generar una orden de compra para solicitar la provisión de 20 rejas de hierro al distribuidor.
- **RF-18: Historial de compras a proveedores.** El sistema debe almacenar el registro de todas las adquisiciones realizadas a distribuidores.

### Módulo de Administración y Seguridad
- **RF-19: Gestión de roles y permisos.** El sistema debe controlar el acceso según roles definidos (Administrador, Ventas, Depósito, Cliente).
- **RF-20: Auditoría y registro de actividad.** El sistema debe guardar un log de acciones críticas realizadas por los usuarios internos.

---

## 2. Requisitos No Funcionales (RNF)

### Seguridad
- **RNF-01:** Las contraseñas de los usuarios deben almacenarse mediante algoritmos de encriptación hash seguros. *Ejemplo:* La clave ingresada por un vendedor no debe guardarse en texto plano en la base de datos de la empresa.
- **RNF-02:** El sistema debe exigir contraseñas con un nivel mínimo de complejidad (al menos 8 caracteres). *Ejemplo:* Impedir que el personal de depósito configure claves inseguras como "123456" en el panel interno.
- **RNF-03:** Todo el tráfico entre el navegador y el servidor debe estar cifrado mediante protocolo HTTPS. *Ejemplo:* Proteger el envío de datos bancarios de los clientes al pagar un portón levadizo.
- **RNF-04:** El panel de administración debe requerir autenticación obligatoria y expiración de sesión tras 15 minutos de inactividad. *Ejemplo:* Si el vendedor deja la computadora del mostrador desatendida, la sesión se cierra automáticamente.

### Rendimiento y Disponibilidad
- **RNF-05:** El tiempo de respuesta en las consultas al catálogo no debe superar los 3 segundos. *Ejemplo:* La grilla de "ventanas de aluminio" debe renderizar fotos y precios en menos de 3 segundos bajo conexiones 4G/móviles.
- **RNF-06:** La actualización de stock tras una venta debe ejecutarse en tiempo real. *Ejemplo:* Si se vende la última cortina roller en la tienda web, el sistema debe marcarla como "Sin stock" inmediatamente para evitar sobreventas en el local.
- **RNF-07:** La plataforma web debe garantizar una disponibilidad (uptime) del 99%. *Ejemplo:* Garantizar que la tienda esté operativa durante fines de semana cuando los clientes minoristas realizan consultas de remodelación.
- **RNF-08:** Se deben programar copias de seguridad (backups) automáticas diarias de la base de datos. *Ejemplo:* Respaldar cada medianoche los registros de ventas, facturas y datos de clientes ante fallos de servidor.

### Usabilidad y Mantenibilidad
- **RNF-09:** La interfaz del panel interno debe ser intuitiva y de fácil uso para personal sin capacitación técnica previa. *Ejemplo:* El encargado de depósito debe poder registrar el ingreso de rejas con un formulario de máximo 3 clics.
- **RNF-10:** El sitio público debe tener diseño responsive (mobile-first). *Ejemplo:* Un arquitecto en obra debe poder navegar el catálogo y consultar cotizaciones cómodamente desde su smartphone.
- **RNF-11:** La arquitectura del sistema debe permitir actualizaciones de código sin interrumpir la operación del servicio.
- **RNF-12:** El código fuente debe estar estructurado modularmente y documentado en el repositorio GitHub.

### Escalabilidad y Normativa
- **RNF-13:** La base de datos debe estar optimizada para soportar el crecimiento del catálogo desde 200 hasta 2.000 productos sin degradar el rendimiento. *Ejemplo:* Búsquedas rápidas aun cuando la empresa incorpore nuevas líneas de aberturas de PVC.
- **RNF-14:** El tratamiento de datos debe cumplir con la Ley 25.326 de Protección de Datos Personales de la República Argentina. *Ejemplo:* Incluir leyenda de consentimiento y permitir al cliente solicitar la baja de sus datos personales.
- **RNF-15:** Los datos personales e historiales de compra de clientes minoristas y mayoristas deben mantenerse bajo estricta confidencialidad.
- **RNF-16:** Se debe garantizar la integridad referencial en la base de datos. *Ejemplo:* Evitar que la eliminación de un proveedor deje huérfanas las órdenes de compra de cortinas enrollables asociadas.