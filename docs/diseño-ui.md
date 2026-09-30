# Diseño UI

## Cobertura de Wireframes
Los wireframes de la plataforma están organizados y referenciados en `diagramas/wireframes/`:
- `01-home-catalogo.svg`: Grilla de catálogo con filtros.
- `02-ficha-producto.svg`: Detalle de producto y selector de cotización a medida.
- `03-carrito.svg`: Listado de compra y solicitud de instalación.
- `04-checkout-pago.svg`: Formulario de datos y pago.
- `05-cuenta-cliente.svg`: Historial de pedidos del cliente.
- `06-login-interno.svg`: Acceso al personal.
- `07-gestion-productos-stock.svg`: Panel de control de inventario.
- `08-gestion-proveedores.svg`: Registro de proveedores.
- `09-gestion-pedidos-ventas.svg`: Control de pedidos en depósito/ventas.
- `10-reportes.svg`: Métricas generales.
- `11-cotizacion-a-medida.svg`: Formulario para pedidos a medida.

---

## Patrones de diseño aplicados

### 1. Catálogo público de aberturas
* **Patrones:** *Grid View*, *Card*, *Faceted Search*.
* **Justificación:** Las Cards presentan fotos, precios y etiquetas de stock de forma rápida. El filtrado agiliza la localización de aberturas.

### 2. Formulario de Cotización a Medida
* **Patrones:** *Input Form*, *File Uploader*, *Inline Validation*.
* **Justificación:** Permite al usuario cargar dimensiones en metros y adjuntar el archivo del plano con validación visual en tiempo real.

### 3. Checkout y Pago
* **Patrones:** *Step-by-Step Wizard*, *Modal Window*.
* **Justificación:** Divide el proceso en pasos claros para reducir errores y abandono de compra.

---

## Accesibilidad concreta (WCAG 2.1)

1. **Contraste de color:** Relación de contraste mínima de 4.5:1 en todos los textos sobre fondos claros.
2. **Áreas táctiles (Tap Targets):** Botones y campos en formato mobile con un tamaño mínimo de 48x48 píxeles.
3. **Navegación por teclado:** Soporte de recorrido por formularios usando `Tab` y `Enter`.