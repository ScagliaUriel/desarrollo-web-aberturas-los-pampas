# Diseño UI

## Cobertura de Wireframes
Los wireframes de la plataforma están organizados y referenciados en `diagramas/wireframes/`[cite: 31]:
- `01-home-catalogo.svg`: Grilla de catálogo con filtros[cite: 31].
- `11-cotizacion-a-medida.svg`: Formulario interactivo para pedidos a medida[cite: 30, 31].

---

## Patrones de diseño aplicados

### 1. Catálogo público de aberturas
* **Patrones:** *Grid View*, *Card*, *Faceted Search*[cite: 31].
* **Justificación orientada al usuario:** Los clientes minoristas navegan prioritariamente desde dispositivos móviles[cite: 30, 31]. Las Cards presentan fotos, precios claros y etiquetas de stock sin recargar la pantalla, facilitando una lectura rápida[cite: 31].

### 2. Formulario de Cotización a Medida
* **Patrones:** *Input Form*, *File Uploader*, *Inline Validation*[cite: 31].
* **Justificación orientada al usuario:** El personal de ventas y los arquitectos/constructoras requieren especificar medidas en milímetros/metros y adjuntar planos[cite: 31]. La validación en línea evita envíos con errores de rango de fabricación[cite: 31].

### 3. Checkout y Pago
* **Patrones:** *Single-Page Express Checkout*, *Modal Notification*[cite: 30, 31].
* **Justificación orientada al usuario:** Se consolida el formulario de envío y la invocación a Mercado Pago en una única vista optimizada[cite: 30, 31] para reducir la fricción cognitiva en usuarios con baja experiencia en e-commerce[cite: 30, 31].

---

## Accesibilidad concreta (WCAG 2.1)

1. **Contraste de color:** Relación de contraste mínima de 4.5:1 en todos los textos sobre fondos claros[cite: 31].
2. **Áreas táctiles (Tap Targets):** Botones y campos en formato mobile con un tamaño mínimo de 48x48 píxeles[cite: 31].
3. **Navegación por teclado:** Soporte de recorrido por formularios usando `Tab` y `Enter`[cite: 31].