# Requisitos del sistema

## Descripción del sistema

Plataforma web de e-commerce y gestión operativa para Aberturas Los Pampas. El sistema resuelve la falta de un canal de venta online, la sincronización manual de stock entre depósito y mostrador, y permite la gestión de cotizaciones de aberturas con dimensiones a medida.

## Requisitos funcionales

### Módulo 1 — Autenticación y Clientes

| ID | Requisito |
|----|-----------|
| RF-01 | El sistema debe permitir el autoregistro de clientes mediante formulario web. |
| RF-02 | El sistema debe permitir el inicio de sesión con correo electrónico y contraseña. |
| RF-03 | El sistema debe permitir a los clientes gestionar y actualizar sus datos del perfil. |
| RF-19 | El sistema debe controlar el acceso según roles (Administrador, Ventas, Depósito, Cliente). |
| RF-20 | El sistema debe guardar un registro de auditoría de las acciones críticas realizadas por los usuarios. |

### Módulo 2 — Catálogo y Cotizaciones

| ID | Requisito |
|----|-----------|
| RF-04 | El sistema debe exhibir el catálogo online con imágenes, descripciones y precios. |
| RF-05 | El sistema debe permitir buscar y filtrar aberturas por categoría y material (chapa, madera, aluminio). |
| RF-06 | El sistema debe mostrar la disponibilidad de stock en tiempo real en la vista de producto. |
| RF-23 | El sistema debe permitir solicitar cotizaciones de aberturas a medida especificando alto, ancho y material. *Ejemplo: Una constructora solicita cotizar una ventana de aluminio de 2.40m x 1.20m.* |

### Módulo 3 — Ventas y Checkout

| ID | Requisito |
|----|-----------|
| RF-07 | El sistema debe permitir agregar productos al carrito y consolidar una compra. |
| RF-08 | El sistema debe procesar cobros integrándose con la API de Mercado Pago. |
| RF-09 | El sistema debe emitir y enviar automáticamente el comprobante de compra por e-mail. |
| RF-10 | El sistema debe permitir al cliente consultar su historial de compras realizadas. |
| RF-21 | El sistema debe permitir registrar y consultar el estado logístico de los pedidos (Pendiente, En preparación, Entregado). |

### Módulo 4 — Stock, Inventario y Proveedores

| ID | Requisito |
|----|-----------|
| RF-11 | El sistema debe permitir el alta de nuevos productos en el catálogo. |
| RF-12 | El sistema debe permitir la modificación de precios, fotos y descripciones. |
| RF-13 | El sistema debe permitir discontinuar o dar de baja productos. |
| RF-14 | El sistema debe descontar automáticamente el stock de la base de datos tras concretarse una venta. |
| RF-15 | El sistema debe emitir notificaciones automáticas cuando un producto alcance el umbral de stock mínimo. |
| RF-16 | El sistema debe permitir la administración de datos de proveedores. |
| RF-17 | El sistema debe permitir generar y gestionar órdenes de compra dirigidas a proveedores. |
| RF-18 | El sistema debe almacenar el historial de órdenes de compra emitidas. |

---

## Requisitos no funcionales

### Rendimiento y disponibilidad

| ID | Requisito |
|----|-----------|
| RNF-05 | El tiempo de respuesta en las consultas del catálogo no debe superar los 3 segundos. *Ejemplo: Renderizar la grilla de productos en menos de 3 segundos bajo redes 4G.* |
| RNF-06 | La actualización de stock tras una compra debe ejecutarse en tiempo real para evitar sobreventas entre el local y la web. |
| RNF-07 | La plataforma web debe garantizar una disponibilidad del 99% de uptime. |
| RNF-08 | Se deben programar copias de seguridad automáticas diarias de la base de datos a la medianoche. |

### Seguridad y usabilidad

| ID | Requisito |
|----|-----------|
| RNF-01 | Las contraseñas de los usuarios deben almacenarse encriptadas mediante algoritmos Hash seguros. |
| RNF-02 | El sistema debe exigir contraseñas con un mínimo de 8 caracteres. *Ejemplo: Impedir que el personal configure claves inseguras como "123456".* |
| RNF-03 | El tráfico entre el cliente y el servidor debe viajar cifrado mediante protocolo HTTPS. |
| RNF-04 | La sesión del panel administrativo debe expirar tras 15 minutos de inactividad por seguridad. |
| RNF-09 | La interfaz interna debe ser intuitiva para personal sin capacitación técnica previa. |
| RNF-10 | El sitio público debe contar con diseño adaptativo (Responsive Design). *Ejemplo: Permitir la consulta del catálogo desde smartphones.* |
| RNF-14 | El tratamiento de datos debe cumplir con la Ley 25.326 de Protección de Datos Personales de Argentina. |
| RNF-16 | El sistema debe garantizar la integridad referencial en la base de datos. *Ejemplo: Impedir eliminar un proveedor que tenga órdenes de compra asociadas.* |