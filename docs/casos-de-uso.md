# Casos de Uso (CU)

Especificación de los principales Casos de Uso del sistema para Aberturas Los Pampas.

## CU-01: Realizar compra de aberturas online

- **Actor Principal:** Cliente Minorista / Mayorista.
- **Precondiciones:** El cliente debe tener productos agregados en el carrito de compras.
- **Garantía de Éxito (Postcondición):** La compra queda registrada, el stock descontado y el cobro procesado.

### Flujo Principal:
1. El cliente accede al carrito de compras y presiona "Proceder al Pago".
2. El sistema solicita los datos de envío/retiro en local.
3. El cliente ingresa la dirección de entrega o selecciona retiro en local.
4. El sistema calcula el monto total y presenta los medios de pago.
5. El cliente selecciona "Mercado Pago" y completa la transacción.
6. El sistema confirma el pago, descuenta las unidades del stock y genera la orden de venta.
7. El sistema muestra la pantalla de confirmación y envía un comprobante por e-mail.

### Flujos Alternativos:
- **5a. Pago Rechazado:** Mercado Pago rechaza la operación por fondos insuficientes o error bancario. El sistema informa el motivo al cliente y le permite seleccionar otro medio de pago sin perder la orden.
- **6a. Sin Stock Suficiente:** Si al momento de pagar otro usuario agotó el stock, el sistema notifica al cliente que el producto pasará a demora de entrega según plazos del proveedor.

---

## CU-02: Gestionar catálogo de productos

- **Actor Principal:** Administrador / Personal de Ventas.
- **Precondiciones:** Usuario autenticado con rol de Administrador.

### Flujo Principal:
1. El administrador ingresa al panel de control y selecciona "Gestión de Productos".
2. El sistema muestra el listado completo de aberturas cargadas.
3. El administrador selecciona "Agregar Producto", completa formulario (tipo, material, medidas, precio, imagen) y guarda.
4. El sistema valida los campos y publica el nuevo producto en el catálogo web.