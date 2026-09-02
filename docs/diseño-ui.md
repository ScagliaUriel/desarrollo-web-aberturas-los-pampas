# Diseño de UI

Descripción de las pantallas principales del sistema web. Los wireframes correspondientes se encuentran en [`/diagramas/wireframes`](../diagramas/wireframes).

## Sitio público (clientes)

### 1. Home / Catálogo
- Grilla de productos con imagen, nombre, tipo, material y precio.
- Filtros por tipo de abertura (portón, puerta, ventana, reja, cortina) y por material (chapa, madera, aluminio, hierro).
- Buscador por texto.
- Accesos a redes sociales de la empresa (Facebook, Instagram).

### 2. Ficha de producto
- Detalle: características, especificaciones, precio, disponibilidad de stock.
- Opción "a medida" cuando el producto lo admite, con campo para indicar dimensiones.
- Botón "Agregar al carrito".
- Aviso de plazo de entrega estimado cuando el producto no tiene stock disponible.

### 3. Carrito de compras
- Listado de productos agregados, cantidad y subtotal.
- Opción de solicitar instalación por producto.
- Botón "Confirmar compra".

### 4. Checkout / Pago
- Resumen del pedido y total.
- Datos de envío/instalación.
- Botón de pago que deriva a Mercado Pago.
- Pantalla de confirmación según el resultado del pago.

### 5. Cuenta del cliente
- Datos personales (o de la empresa, si es mayorista).
- Historial de pedidos con estado (pendiente de pago / pagado / entregado).
- Estado de instalaciones solicitadas.

## Panel interno (vendedor / stock / administrador)

### 6. Login interno
- Acceso diferenciado por usuario y contraseña, con rol asignado (vendedor, stock, administrador).

### 7. Gestión de productos y stock
- ABM de productos (alta, baja, modificación).
- Edición de cantidades en stock.
- Alertas de stock bajo o agotado.

### 8. Gestión de proveedores
- ABM de proveedores y sus datos de facturación.
- Generación de órdenes de compra, con selección de productos, cantidades y plazo de entrega.
- Historial de compras por proveedor.

### 9. Gestión de pedidos y ventas
- Listado de pedidos con filtro por estado.
- Detalle de cada pedido (productos, cliente, pago, instalación).

### 10. Reportes
- Ventas del mes (totales, cantidad de pedidos).
- Productos más vendidos, para apoyar decisiones de compra a proveedores.

## Lineamientos generales

- Diseño simple y con lenguaje claro, considerando que el personal actual no tiene experiencia previa con sistemas de gestión.
- Prioridad mobile-first en el sitio público, ya que buena parte de los clientes (minoristas) probablemente naveguen desde el celular.
- El panel interno debe minimizar la posibilidad de error dado que hoy no hay usuarios diferenciados ni capacitación en el uso de sistemas.