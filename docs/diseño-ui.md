# Diseño UI

## Cobertura de Wireframes
Los wireframes de la plataforma están organizados en `diagramas/wireframes/` y representan la versión actual del prototipo funcional:

- `01-home-catalogo.svg`: home del catálogo con productos destacados, filtros por categoría, material y rango de precio, y llamado a la acción para cotizar a medida (CU-01, CU-03).
- `02-ficha-producto.svg`: ficha de producto con detalle y stock disponible (CU-01).
- `03-carrito.svg`: carrito de compras (CU-04).
- `04-checkout-pago.svg`: checkout con Mercado Pago o transferencia bancaria (CU-05, CU-06).
- `05-cuenta-cliente.svg`: cuenta del cliente con el historial y el estado de sus pedidos y cotizaciones (CU-07).
- `06-login-interno.svg`: ingreso del personal interno; el rol lo determina la cuenta (CU-03).
- `07-gestion-productos-stock.svg`: gestión de productos y stock para el operador de depósito (CU-08).
- `08-gestion-proveedores.svg`: gestión de proveedores y órdenes de compra (CU-11, CU-14).
- `09-gestion-pedidos-ventas.svg`: control de pedidos y despachos, y coordinación de instalaciones (CU-09, CU-10).
- `10-reportes.svg`: dashboard de ventas y reportes (CU-12).
- `11-cotizacion-a-medida.svg`: formulario de cotización con tipología, dimensiones, material, vidrio, color, plano técnico opcional, observaciones y resumen estimado (CU-02).

---

## Patrones de diseño aplicados

### 1. Catálogo público de aberturas
* **Patrones:** *Grid View*, *Card*, *CTA-first*, *Faceted Search*.
* **Justificación orientada al usuario:** Los clientes minoristas se desplazan prioritariamente desde dispositivos móviles. Las cards muestran producto, imagen, precio y acción de compra o cotización, reduciendo la cantidad de decisiones en la primera vista. Los filtros por categoría, material y rango de precio permiten encontrar rápidamente el producto buscado.

### 2. Formulario de Cotización a Medida
* **Patrones:** *Input Form*, *Summary Panel*, *Inline Validation*, *File Uploader*.
* **Justificación orientada al usuario:** El cliente debe completar una solicitud con dimensiones, material, vidrio y acabado, y recibir un resumen estimado antes de enviar. La validación inmediata ayuda a evitar errores comunes en medidas y valores no válidos. El campo de plano técnico opcional permite adjuntar plano técnico cuando se requiere.

### 3. Checkout y Pago
* **Patrones:** *Single-Page Express Checkout*, *Modal Notification*.
* **Justificación orientada al usuario:** Se consolida el flujo de confirmación y pago para reducir fricción cognitiva, especialmente en usuarios con poca experiencia en e-commerce.

---

## Accesibilidad concreta (WCAG 2.1)

1. **Contraste de color:** Relación de contraste mínima de 4.5:1 en todos los textos sobre fondos claros.
2. **Áreas táctiles (Tap Targets):** Botones y campos en formato mobile con un tamaño mínimo de 48x48 píxeles.
3. **Navegación por teclado:** Soporte de recorrido por formularios usando `Tab` y `Enter`.
4. **Jerarquía visual:** títulos, etiquetas y estados claros para distinguir pantallas de catálogo, checkout y panel interno.