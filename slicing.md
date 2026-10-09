# Ejercicio: partir una épica en slices verticales

## La épica

> Como cliente de Aberturas Los Pampas, quiero abonar mi compra de forma digital desde la plataforma web, para recibir la confirmación de mi pedido inmediatamente sin necesidad de utilizar efectivo o dirigirme al local[cite: 31].

---

## Parte A — Historias verticales

### Historia 1 — Pago mediante transferencia bancaria (MVP)
Como cliente, quiero visualizar los datos bancarios al finalizar la orden, para transferir el dinero e informar el pago[cite: 31].

**Criterios de aceptación**
1. **Dado** que el cliente elige "Transferencia", **cuando** confirma la orden, **entonces** el sistema le despliega el CBU, Alias y CUIT de la empresa[cite: 31].
2. **Dado** que el cliente visualiza los datos bancarios, **cuando** presiona "Notificar transferencia", **entonces** el sistema cambia el estado del pedido a "Verificando transferencia"[cite: 30, 31].

---

### Historia 2 — Cobro digital con tarjeta vía pasarela de pago
Como cliente, quiero pagar con tarjeta de crédito/débito a través de Mercado Pago, para confirmar el cobro en tiempo real[cite: 31].

**Criterios de aceptación**
1. **Dado** que el cliente elige Mercado Pago y la tarjeta es aprobada, **cuando** finaliza la operación, **entonces** la orden cambia a "Pagada" y se descuenta el stock[cite: 31].
2. **Dado** que el pago es rechazado por la entidad emisora, **cuando** concluye la transacción, **entonces** el sistema informa el rechazo y conserva la orden en "Pendiente de pago"[cite: 30, 31].

---

### Historia 3 — Descuento automático de stock e integración de depósito
Como encargado de depósito, quiero que el sistema descuente las unidades del stock inmediatamente al aprobarse el pago, para evitar la sobreventa y comenzar la preparación física del despacho[cite: 30, 31].

**Criterios de aceptación**
1. **Dado** que el Webhook de la pasarela confirma el pago, **cuando** se actualiza la orden, **entonces** el sistema descuenta las unidades de forma atómica[cite: 31].
2. **Dado** que un producto alcanza su stock mínimo tras el cobro, **cuando** la transacción finaliza, **entonces** el sistema notifica automáticamente al depósito para reposición[cite: 30, 31].

---

### Historia 4 — Emisión y envío automático de comprobantes
Como cliente, quiero recibir mi comprobante por correo electrónico al confirmarse el pago, para disponer de un respaldo[cite: 31].

**Criterios de aceptación**
1. **Dado** que el pago pasa a "Aprobado", **cuando** se registra la transacción, **entonces** el sistema envía la factura digital en PDF al e-mail del cliente[cite: 31].
2. **Dado** que el envío del e-mail falla, **cuando** se registra el error, **entonces** el sistema encola el envío para reintento automático sin afectar la compra[cite: 30, 31].

---

### Historia 5 — Reintento de pago para órdenes pendientes
Como cliente con un pago rechazado, quiero reintentar el abono desde mi perfil, para no tener que volver a cargar los artículos al carrito[cite: 31].

**Criterios de aceptación**
1. **Dado** un pedido en estado "Pendiente de pago", **cuando** el cliente presiona "Reintentar pago", **entonces** el sistema abre nuevamente el checkout[cite: 31].
2. **Dado** que el cliente elige un nuevo medio de pago válido, **cuando** la pasarela lo aprueba, **entonces** la orden actualiza su estado a "Pagada"[cite: 30, 31].

---

## Parte B — Los caminos que no salen bien

**Historia elegida:** Historia 2 — Cobro digital con tarjeta vía pasarela de pago[cite: 31]

| Pregunta | Qué hace el sistema | Quién decide | Justificación de la decisión |
|----------|----------------------|--------------|------------------------------|
| ¿Qué pasa si el saldo es insuficiente? | Notifica el rechazo sin vaciar el carrito, registra la orden en "Pendiente" y ofrece reintentar[cite: 31]. | **Negocio** | Es una política comercial para facilitar la conversión y dar al cliente la oportunidad de usar otro medio[cite: 31]. |
| ¿Qué pasa si el producto queda sin stock durante el checkout? | Cancela la operación antes de invocar la API de pago y alerta *"Stock agotado mientras realizaba la compra"*[cite: 31]. | **Analista** | Es una regla de comportamiento funcional que protege la consistencia del catálogo ante concurrencia[cite: 31]. |
| ¿Qué pasa si la pasarela descuenta el saldo pero falla el webhook de confirmación? | Mantiene la transacción en un log de contingencia y ejecuta un proceso de conciliación automática[cite: 31]. | **Técnica** | Es un mecanismo de arquitectura para garantizar la integridad eventual de las transacciones financieras[cite: 31]. |
| ¿Qué pasa si el cliente presiona el botón "Pagar" dos veces seguidas? | Deshabilita el botón tras el primer clic e implementa un token de idempotencia en la solicitud[cite: 31]. | **Técnica** | Es un patrón de diseño técnico para prevenir cargos dobles y duplicación de peticiones HTTP[cite: 31]. |
| ¿Qué pasa si se interrumpe la conexión a Internet del cliente tras ingresar la tarjeta? | La pasarela procesa el cobro de forma asincrónica e impacta la orden mediante Webhook[cite: 31]. | **Técnica** | Responde a la tolerancia a fallos de la red para evitar transacciones inconsistentes[cite: 31]. |