# Ejercicio de Story Slicing: Billetera Virtual y Catálogo

Demostración de la técnica de slicing (división vertical de historias de usuario) aplicada a la plataforma de Aberturas Los Pampas.

## Épica principal: Gestión de pagos y catálogo online

### Parte A — Estrategia de Slicing (Tajadas Verticales)
Se divide la funcionalidad en entregas incrementales que aportan valor de negocio desde el primer corte, evitando capas horizontales (solo backend o solo frontend).

1. **Slicing 1 (MVP - Cobro básico manual):** El cliente puede visualizar el catálogo de aberturas y solicitar la compra mediante transferencia bancaria con envío manual de comprobante.
2. **Slicing 2 (Integración Mercado Pago Sandbox):** El cliente puede pagar directamente en el checkout utilizando la pasarela de Mercado Pago (tarjetas de crédito/débito).
3. **Slicing 3 (Gestión de comprobantes y estado):** Se automatiza el cambio de estado de la compra (Aprobado/Rechazado) y la emisión del comprobante digital.

---

## Parte B — Historias de Usuario Derivadas del Slicing

### HU-SL-01: Visualización y compra básica por transferencia
- **Como** cliente de Aberturas Los Pampas  
- **Quiero** seleccionar un producto del catálogo y obtener los datos bancarios para transferir  
- **Para** concretar una compra sin necesidad de asistir al local  

**Criterios de Aceptación:**
- **Dado que** el cliente selecciona una ventana o puerta  
- **Cuando** confirma el pedido con método "Transferencia"  
- **Entonces** el sistema muestra los datos de CBU/Alias y el código de pedido generado.

### HU-SL-02: Pago integrado con Mercado Pago
- **Como** cliente minorista  
- **Quiero** pagar mi pedido mediante Mercado Pago en la web  
- **Para** recibir la confirmación de mi compra de forma inmediata  

**Criterios de Aceptación:**
- **Dado que** el cliente está en la pantalla de pago  
- **Cuando** elige Mercado Pago y completa la transacción de forma exitosa  
- **Entonces** el sistema registra el cobro y redirige a la pantalla de éxito.