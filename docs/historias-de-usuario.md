# Historias de Usuario (HU)

Listado de Historias de Usuario para la plataforma web de Aberturas Los Pampas, redactadas bajo el formato estándar y con Criterios de Aceptación.

## Módulo: Catálogo y Búsqueda

### HU-01: Consulta de catálogo de aberturas
- **Como** cliente minorista o mayorista  
- **Quiero** navegar por el catálogo filtrando por tipo de abertura (chapa, madera, aluminio)  
- **Para** encontrar rápidamente el producto que necesito con sus especificaciones técnicas y precio.

**Criterios de Aceptación:**
- **Dado que** el usuario ingresa a la sección de catálogo  
- **Cuando** selecciona la categoría "Ventanas de Aluminio"  
- **Entonces** la plataforma muestra únicamente las ventanas fabricadas en dicho material con su precio actualizado.

---

### HU-02: Búsqueda por texto libre
- **Como** cliente  
- **Quiero** buscar productos ingresando palabras clave en una barra de búsqueda  
- **Para** localizar aberturas específicas sin recorrer todo el sitio.

**Criterios de Aceptación:**
- **Dado que** el cliente escribe "portón levadizo" en el buscador  
- **Cuando** presiona la tecla Enter o el icono de búsqueda  
- **Entonces** el sistema lista todos los portones levadizos disponibles.

---

## Módulo: Ventas y Checkout

### HU-03: Integración de pago con Mercado Pago
- **Como** cliente  
- **Quiero** abonar mi carrito de compras mediante la pasarela de Mercado Pago  
- **Para** utilizar tarjetas de crédito, débito o dinero en cuenta de forma segura.

**Criterios de Aceptación:**
- **Dado que** el cliente tiene productos en su carrito  
- **Cuando** inicia el proceso de pago y selecciona Mercado Pago  
- **Entonces** el sistema procesa la transacción mediante la API y retorna el estado del pago (Aprobado/Rechazado).

---

## Módulo: Stock e Inventario

### HU-04: Actualización automática de stock
- **Como** encargado de stock  
- **Quiero** que el sistema descuente automáticamente las unidades vendidas en la web  
- **Para** mantener las existencias reales reflejadas en el local y la plataforma.

**Criterios de Aceptación:**
- **Dado que** hay 5 unidades en stock de una puerta de chapa  
- **Cuando** un cliente compra 2 unidades mediante la web  
- **Entonces** el sistema actualiza el stock disponible a 3 unidades inmediatamente.