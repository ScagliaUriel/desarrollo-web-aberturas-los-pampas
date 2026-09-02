# Requisitos

Requisitos iniciales relevados a partir del análisis preliminar de Aberturas Los Pampas. Se organizan por área funcional, según el diagnóstico realizado (Ventas, Redes, Clientes, Proveedores, Stock) y por requisitos no funcionales derivados del diagnóstico de infraestructura y seguridad.

## Requisitos funcionales

### Catálogo y ventas

- **RF-01:** El sistema debe permitir publicar un catálogo online de productos (portones, puertas, ventanas en chapa/madera/aluminio, rejas de hierro, cortinas enrollables y roller), en formato estándar y a medida.
- **RF-02:** Cada producto del catálogo debe mostrar tipo de abertura, características, especificaciones y precio.
- **RF-03:** El sistema debe integrarse con Mercado Pago para procesar los cobros de las ventas realizadas online.
- **RF-04:** El sistema debe diferenciar condiciones de venta para clientes minoristas y mayoristas.
- **RF-05:** El sistema debe permitir solicitar servicios de instalación o subcontratación asociados a un producto.

### Redes sociales

- **RF-06:** El catálogo web debe poder vincularse con las redes sociales de la empresa (Facebook, Instagram, etc.) para difundir productos.

### Clientes

- **RF-07:** El sistema debe permitir el alta y gestión de usuarios/clientes.
- **RF-08:** Cada cliente debe poder acceder a sus datos de compra, envío e instalación de materiales.
- **RF-09:** El sistema debe generar una visión consolidada de las ventas realizadas por mes.

### Proveedores

- **RF-10:** El sistema debe permitir el alta y gestión de proveedores, incluyendo datos necesarios para la facturación.
- **RF-11:** El sistema debe permitir generar órdenes de compra a proveedores, con sus plazos de entrega.
- **RF-12:** El sistema debe mantener un historial de compras por proveedor.
- **RF-13:** El sistema debe permitir generar reportes de los productos más vendidos, en base al historial de compras y ventas.

### Stock

- **RF-14:** El sistema debe reflejar en el catálogo online las cantidades exactas en stock de cada producto.
- **RF-15:** El sistema debe permitir la compra de productos sin stock disponible, sujeta a los plazos de entrega de los proveedores correspondientes.

## Requisitos no funcionales

- **RNF-01 (Seguridad):** El sistema debe contemplar usuarios diferenciados con contraseñas seguras, dado que actualmente el uso de los equipos es indiscriminado y sin perfiles definidos.
- **RNF-02 (Seguridad):** Las credenciales de acceso al sistema y a la red no deben reutilizar contraseñas estándar/compartidas, como ocurre hoy con el Wi-Fi y los celulares comerciales.
- **RNF-03 (Disponibilidad):** El sistema debe funcionar de forma estable sobre la conexión a internet actual de la empresa (100 Mbps, Claro), considerando que no existe red segmentada entre el personal y visitantes.
- **RNF-04 (Usabilidad):** El sistema debe ser utilizable por personal sin capacitación previa en informática ni en seguridad de la información.
- **RNF-05 (Mantenibilidad):** El sistema debe poder operarse desde equipos actualmente desactualizados (computadoras de escritorio de ventas y stock), sin requerir hardware de alta gama.
- **RNF-06 (Escalabilidad):** El sistema debe permitir incorporar en el futuro nuevos canales (por ejemplo, más redes sociales) sin rediseñar el catálogo base.

## Fuera de alcance (por ahora)

- Reestructuración de la infraestructura eléctrica del local (estabilizador de tensión, división de circuitos).
- Capacitación formal del personal en ciberseguridad.
- Reemplazo del hardware existente (computadoras, celulares comerciales).

> Estos puntos surgen del diagnóstico de infraestructura tecnológica, pero no son requisitos del sistema web en sí, sino recomendaciones organizacionales relevadas durante el análisis preliminar.