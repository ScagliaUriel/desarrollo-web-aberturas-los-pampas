# Ejercicio: partir una épica en slices verticales

## La épica

> Como cliente de Aberturas Los Pampas, quiero abonar mi compra de forma digital desde la plataforma web, para recibir la confirmación de mi pedido inmediatamente sin necesidad de utilizar efectivo o dirigirme al local.

---

## Parte A — Historias verticales

### Historia 1 — Pago mediante transferencia bancaria (MVP)
Como cliente, quiero visualizar los datos bancarios al finalizar la orden, para transferir el dinero e informar el pago.

**Criterios de aceptación**
1. **Dado** que el cliente elige "Transferencia", **cuando** confirma la orden, **entonces** el sistema le despliega el CBU, Alias y CUIT de la empresa.

---

### Historia 2 — Cobro digital con tarjeta vía pasarela de pago
Como cliente, quiero pagar con tarjeta de crédito/débito a través de Mercado Pago, para confirmar el cobro en tiempo real.

**Criterios de aceptación**
1. **Dado** que el cliente elige Mercado Pago y la tarjeta es aprobada, **cuando** finaliza la operación, **entonces** la orden cambia a "Pagada" y se descuenta el stock.

---

### Historia 3 — Actualización automática de stock tras cobro exitoso
Como encargado de depósito, quiero que el sistema descuente las unidades del stock inmediatamente al aprobarse el pago, para evitar la sobreventa.

**Criterios de aceptación**
1. **Dado** que el Webhook de la pasarela confirma el pago, **cuando** se actualiza la orden, **entonces** el sistema descuenta las unidades de forma atómica.

---

### Historia 4 — Emisión y envío automático de comprobantes
Como cliente, quiero recibir mi comprobante por correo electrónico al confirmarse el pago, para disponer de un respaldo.

**Criterios de aceptación**
1. **Dado** que el pago pasa a "Aprobado", **cuando** se registra la transacción, **entonces** el sistema envía la factura digital en PDF al e-mail del cliente.

---

### Historia 5 — Reintento de pago para órdenes pendientes
Como cliente con un pago rechazado, quiero reintentar el abono desde mi perfil, para no tener que volver a cargar los artículos al carrito.

**Criterios de aceptación**
1. **Dado** un pedido en estado "Pendiente de pago", **cuando** el cliente presiona "Reintentar pago", **entonces** el sistema abre nuevamente el checkout.

---

## Parte B — Los caminos que no salen bien

**Historia elegida:** Historia 2 — Cobro digital con tarjeta vía pasarela de pago

| Pregunta | Qué hace el sistema | Quién decide | Justificación de la decisión |
|----------|----------------------|--------------|------------------------------|
| ¿Qué pasa si el saldo es insuficiente? | Notifica el rechazo sin vaciar el carrito, registra la orden en "Pendiente" y ofrece reintentar. | **Negocio** | Es una política comercial para facilitar la conversión y dar al cliente la oportunidad de usar otro medio. |
| ¿Qué pasa si el producto queda sin stock durante el checkout? | Cancela la operación antes de invocar la API de pago y alerta *"Stock agotado mientras realizaba la compra"*. | **Analista** | Es una regla de comportamiento funcional que protege la consistencia del catálogo ante concurrencia. |
| ¿Qué pasa si la pasarela descuenta el saldo pero falla el webhook de confirmación? | Mantiene la transacción en un log de contingencia y ejecuta un proceso de conciliación automática. | **Técnica** | Es un mecanismo de arquitectura para garantizar la integridad eventual de las transacciones financieras. |
| ¿Qué pasa si el cliente presiona el botón "Pagar" dos veces seguidas? | Deshabilita el botón tras el primer clic e implementa un token de idempotencia en la solicitud. | **Técnica** | Es un patrón de diseño técnico para prevenir cargos dobles y duplicación de peticiones HTTP. |
| ¿Qué pasa si se interrumpe la conexión a Internet del cliente tras ingresar la tarjeta? | La pasarela procesa el cobro de forma asincrónicas e impacta la orden mediante Webhook. | **Técnica** | Responde a la tolerancia a fallos de la red para evitar transacciones inconsistentes. |