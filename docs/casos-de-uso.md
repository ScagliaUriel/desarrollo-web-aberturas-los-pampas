# Casos de Uso

## Actores

| Actor | Descripción |
| ----- | ----------- |
| Cliente | Persona o negocio (minorista o mayorista) que consulta el catálogo y realiza compras. |
| Vendedor | Personal del sector de ventas; atiende clientes y gestiona pedidos. |
| Encargado de Stock | Personal del sector de stock; mantiene actualizadas las cantidades disponibles. |
| Administrador | Propietario(s); gestiona usuarios, proveedores y reportes generales. |
| Mercado Pago | Sistema externo que procesa los pagos de las ventas. |

## Listado de casos de uso

| ID | Caso de uso | Actor(es) principal(es) |
| -- | ----------- | ------------------------ |
| CU-01 | Consultar catálogo de productos | Cliente |
| CU-02 | Filtrar / buscar productos | Cliente |
| CU-03 | Registrarse en el sistema | Cliente |
| CU-04 | Iniciar sesión | Cliente, Vendedor, Encargado de Stock, Administrador |
| CU-05 | Agregar producto al carrito | Cliente |
| CU-06 | Confirmar compra (checkout) | Cliente |
| CU-07 | Pagar con Mercado Pago | Cliente, Mercado Pago |
| CU-08 | Solicitar instalación de un producto | Cliente |
| CU-09 | Consultar historial de compras propio | Cliente |
| CU-10 | Gestionar productos (alta/baja/modificación) | Encargado de Stock, Administrador |
| CU-11 | Actualizar stock disponible | Encargado de Stock |
| CU-12 | Gestionar proveedores (alta/baja/modificación) | Administrador |
| CU-13 | Generar orden de compra a proveedor | Administrador, Encargado de Stock |
| CU-14 | Consultar historial de compras a proveedores | Administrador |
| CU-15 | Ver reporte de ventas mensuales | Administrador |
| CU-16 | Ver reporte de productos más vendidos | Administrador |
| CU-17 | Gestionar usuarios del sistema | Administrador |

## Descripción de casos de uso principales

### CU-06 — Confirmar compra (checkout)
- **Actor principal:** Cliente
- **Precondición:** El cliente tiene al menos un producto en el carrito y una sesión iniciada.
- **Flujo principal:**
  1. El cliente revisa los productos del carrito (cantidad, precio, subtotal).
  2. El cliente indica si requiere instalación (CU-08).
  3. El cliente selecciona método de pago (Mercado Pago).
  4. El sistema deriva el pago a Mercado Pago (CU-07).
  5. El sistema registra el pedido con estado "pendiente de pago".
- **Flujo alternativo:** Si algún producto no tiene stock, el sistema informa el plazo de entrega estimado y permite confirmar igual (compra sujeta a reposición).
- **Postcondición:** Se genera un pedido asociado al cliente, con su detalle de productos.

### CU-07 — Pagar con Mercado Pago
- **Actores:** Cliente, Mercado Pago
- **Precondición:** Existe un pedido en estado "pendiente de pago".
- **Flujo principal:**
  1. El sistema redirige al cliente al checkout de Mercado Pago con el monto del pedido.
  2. El cliente completa el pago en la plataforma externa.
  3. Mercado Pago notifica el resultado al sistema.
  4. El sistema actualiza el estado del pedido (pagado / rechazado).
- **Postcondición:** El pedido queda con su estado de pago actualizado.

### CU-13 — Generar orden de compra a proveedor
- **Actor principal:** Administrador / Encargado de Stock
- **Precondición:** El proveedor y los productos a reponer ya están dados de alta en el sistema.
- **Flujo principal:**
  1. Se selecciona el proveedor.
  2. Se agregan los productos y cantidades a solicitar.
  3. Se indica el plazo de entrega acordado.
  4. El sistema guarda la orden de compra asociada al proveedor.
- **Postcondición:** Queda registrada la orden de compra, disponible en el historial del proveedor (CU-14).

Ver el diagrama de casos de uso en [`/diagramas/casos-de-uso.puml`](../diagramas/casos-de-uso.puml).