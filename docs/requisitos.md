# Requisitos del sistema

## Descripción del sistema

Plataforma web de e-commerce y gestión operativa para Aberturas Los Pampas. El sistema resuelve el canal de venta online, sincroniza en tiempo real el inventario entre mostrador y depósito, y permite solicitar presupuestos de aberturas a medida.

---

## Requisitos funcionales

### Módulo 1 — Autenticación, Usuarios y Seguridad
| ID | Requisito |
|----|-----------|
| RF-01 | El sistema debe permitir el autoregistro de clientes minoristas y mayoristas mediante formulario web. |
| RF-02 | El sistema debe permitir el inicio de sesión mediante e-mail y contraseña. |
| RF-03 | El sistema debe permitir la gestión y actualización del perfil de usuario y direcciones de entrega. |
| RF-04 | El sistema debe controlar el acceso a pantallas e interfaces según el rol asignado (Cliente, Ventas, Depósito, Administrador). |
| RF-05 | El sistema debe registrar en un log de auditoría las acciones críticas del sistema (modificaciones de precios, cambios de stock y fully anulaciones). |

### Módulo 2 — Catálogo y Cotizaciones a Medida
| ID | Requisito |
|----|-----------|
| RF-06 | El sistema debe exhibir el catálogo online con fotos, especificaciones y precios actualizados. |
| RF-07 | El sistema debe permitir filtrar productos por categoría, material (aluminio, madera, chapa) y rango de precio. |
| RF-08 | El sistema debe mostrar el stock disponible en tiempo real en la vista de producto. |
| RF-09 | El sistema debe permitir solicitar presupuestos para aberturas con dimensiones a medida (alto, ancho, material, vidrio y planos adjuntos). |

### Módulo 3 — Ventas, Checkout y Logística
| ID | Requisito |
|----|-----------|
| RF-10 | El sistema debe permitir agregar productos al carrito y consolidar una orden de compra. |
| RF-11 | El sistema debe integrar la pasarela de pagos digitales (Mercado Pago) para el cobro online. |
| RF-12 | El sistema debe emitir y enviar automáticamente la factura/comprobante de compra por e-mail al cliente. |
| RF-13 | El sistema debe permitir al cliente consultar el historial y el estado logístico de sus pedidos (Pendiente, En preparación, Despachado, Entregado). |

### Módulo 4 — Stock, Depósito y Proveedores
| ID | Requisito |
|----|-----------|
| RF-14 | El sistema debe permitir la gestión del catálogo (alta, baja y modificación de artículos). |
| RF-15 | El sistema debe descontar automáticamente del inventario las unidades vendidas tras la aprobación del pago. |
| RF-16 | El sistema debe emitir notificaciones automáticas al encargado cuando un producto alcance su umbral de stock mínimo. |
| RF-17 | El sistema debe permitir administrar los datos de contacto y rubro de los proveedores. |
| RF-18 | El sistema debe permitir emitir, consultar y registrar órdenes de compra dirigidas a los proveedores para reposición de stock. |
| RF-19 | El sistema debe permitir registrar y coordinar la colocación/instalación técnica de aberturas contratada por el cliente. |

---

## Requisitos no funcionales

### Rendimiento y Disponibilidad
| ID | Requisito |
|----|-----------|
| RNF-01 | El tiempo de respuesta en la navegación del catálogo no debe superar los 3 segundos bajo conexiones móviles 4G. |
| RNF-02 | El descuento de stock en la base de datos debe realizarse de forma atómica en tiempo real para evitar sobreventas. |
| RNF-03 | El sistema debe garantizar una disponibilidad (uptime) del 99% anual. |
| RNF-04 | Se deben realizar respaldos (backups) automáticos diarios de la base de datos a las 02:00 hs. |

### Seguridad
| ID | Requisito |
|----|-----------|
| RNF-05 | Las contraseñas deben almacenarse encriptadas mediante algoritmos Hash seguros (bcrypt). |
| RNF-06 | La contraseña debe requerir un mínimo de 8 caracteres, al menos un número y una mayúscula. |
| RNF-07 | La transmisión de datos debe realizarse obligatoriamente mediante protocolo seguro HTTPS. |
| RNF-08 | Las sesiones de los usuarios administradores deben expirar tras 15 minutos de inactividad. |

### Usabilidad, Accesibilidad y Mantenibilidad
| ID | Requisito |
|----|-----------|
| RNF-09 | El panel interno debe requerir un máximo de 3 clics para completar tareas frecuentes. |
| RNF-10 | El sitio público debe contar con diseño responsivo adaptado a dispositivos móviles (Mobile-First). |
| RNF-11 | La interfaz debe cumplir con criterios de accesibilidad como contraste de colores mínimo 4.5:1 y áreas táctiles de 48px. |
| RNF-12 | Las actualizaciones del sistema deben desplegarse sin interrumpir el servicio (Zero-Downtime Deployment). |
| RNF-13 | El código fuente debe estructurarse de manera modular y documentarse en el repositorio de GitHub. |

### Escalabilidad y Normativa
| ID | Requisito |
|----|-----------|
| RNF-14 | La base de datos debe soportar hasta 5.000 productos y 100.000 pedidos sin degradar respuesta. |
| RNF-15 | El tratamiento de datos debe cumplir con la Ley 25.326 de Protección de Datos Personales de Argentina. |
| RNF-16 | El modelo de datos debe mantener la integridad referencial para evitar registros huérfanos. |