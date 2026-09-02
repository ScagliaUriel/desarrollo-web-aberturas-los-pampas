# Modelo Entidad-Relación

Modelo de datos preliminar derivado de los requisitos funcionales del sistema. Diagrama fuente en [`/diagramas/er.puml`](../diagramas/er.puml).

## Entidades

### Usuario
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_usuario | PK | Identificador único |
| nombre | string | Nombre completo |
| email | string | Usado para login |
| contraseña | string | Hasheada |
| rol | enum | cliente / vendedor / stock / administrador |

### Cliente
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_cliente | PK | Identificador único |
| id_usuario | FK → Usuario | Cuenta asociada |
| tipo_cliente | enum | minorista / mayorista |
| razon_social | string | Solo mayoristas (ferreterías, corralones, constructoras, estudios de arquitectura, etc.) |
| cuit | string | Opcional, para facturación a mayoristas |
| dirección | string | Dirección de envío/instalación |

### Producto
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_producto | PK | Identificador único |
| nombre | string | Nombre del producto |
| tipo | enum | portón / puerta / ventana / reja / cortina enrollable / cortina roller |
| material | enum | chapa / madera / aluminio / hierro |
| a_medida | boolean | Si admite fabricación a medida |
| descripción | text | Características y especificaciones |
| precio | decimal | Precio de venta |
| stock_actual | int | Cantidad disponible |

### Pedido
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_pedido | PK | Identificador único |
| id_cliente | FK → Cliente | Cliente que realiza el pedido |
| fecha | datetime | Fecha del pedido |
| estado | enum | pendiente de pago / pagado / rechazado / entregado |
| total | decimal | Monto total |

### DetallePedido
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_detalle | PK | Identificador único |
| id_pedido | FK → Pedido | Pedido al que pertenece |
| id_producto | FK → Producto | Producto solicitado |
| cantidad | int | Cantidad pedida |
| precio_unitario | decimal | Precio al momento de la compra |
| medida_a_medida | string | Medidas si el producto es a medida (opcional) |

### Pago
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_pago | PK | Identificador único |
| id_pedido | FK → Pedido | Pedido asociado |
| id_mercadopago | string | Identificador de la transacción en Mercado Pago |
| monto | decimal | Monto abonado |
| estado | enum | aprobado / pendiente / rechazado |

### Instalacion
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_instalacion | PK | Identificador único |
| id_pedido | FK → Pedido | Pedido asociado |
| tipo | enum | propia / subcontratada |
| fecha_programada | date | Fecha estimada de instalación |
| estado | enum | pendiente / realizada |

### Proveedor
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_proveedor | PK | Identificador único |
| razon_social | string | Nombre del proveedor |
| cuit | string | Datos de facturación |
| contacto | string | Teléfono / email |

### OrdenCompra
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_orden | PK | Identificador único |
| id_proveedor | FK → Proveedor | Proveedor al que se le realiza la orden |
| fecha | date | Fecha de emisión |
| plazo_entrega | date | Fecha estimada de entrega |
| estado | enum | pendiente / recibida |

### DetalleOrdenCompra
| Campo | Tipo | Descripción |
| ----- | ---- | ----------- |
| id_detalle_orden | PK | Identificador único |
| id_orden | FK → OrdenCompra | Orden a la que pertenece |
| id_producto | FK → Producto | Producto solicitado al proveedor |
| cantidad | int | Cantidad solicitada |
| precio_unitario | decimal | Costo acordado con el proveedor |

## Relaciones principales

- Un **Usuario** puede ser un **Cliente** (1:1, cuando el rol es "cliente").
- Un **Cliente** realiza muchos **Pedidos** (1:N).
- Un **Pedido** tiene muchos **DetallePedido**, y cada detalle referencia un **Producto** (N:M resuelto vía DetallePedido).
- Un **Pedido** tiene un **Pago** asociado (1:1).
- Un **Pedido** puede tener una **Instalacion** asociada (1:1, opcional).
- Un **Proveedor** recibe muchas **OrdenCompra** (1:N).
- Una **OrdenCompra** tiene muchos **DetalleOrdenCompra**, y cada detalle referencia un **Producto** (N:M resuelto vía DetalleOrdenCompra).
- Un **Producto** puede aparecer en muchos **DetallePedido** y muchos **DetalleOrdenCompra**.