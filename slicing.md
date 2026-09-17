# Ejercicio: partir una épica en slices verticales

## La épica

> Como cliente de la billetera, quiero enviar dinero a otro usuario de la app para pagarle sin usar efectivo.

---

## Parte A — Historias verticales

### Historia 1 — Envío de dinero a un contacto de la agenda con saldo suficiente

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario de la billetera, quiero seleccionar un contacto de mi agenda y enviarle un monto disponible en mi saldo, para transferirle dinero de forma rápida. |

**Criterios de aceptación**

1. **Dado** que el usuario posee saldo suficiente y elige un contacto con cuenta activa, **cuando** confirma la transferencia, **entonces** el sistema descuenta el monto de su cuenta, lo acredita en la cuenta destino y emite un comprobante.
2. **Dado** que el monto a transferir supera el saldo disponible, **cuando** el usuario intenta confirmar, **entonces** el sistema bloquea la acción y muestra *"Saldo insuficiente para realizar la transferencia"*.

---

### Historia 2 — Envío de dinero ingresando CVU o Alias manualmente

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario de la billetera, quiero ingresar un CVU o Alias de destino, para transferir dinero a una persona que no tengo guardada en mis contactos. |

**Criterios de aceptación**

1. **Dado** que el usuario ingresa un CVU o Alias válido de 22 dígitos o texto, **cuando** presiona "Buscar", **entonces** el sistema muestra el nombre y CUIT del destinatario para confirmar la operación.
2. **Dado** que el CVU o Alias ingresado no existe en la red, **cuando** se ejecuta la búsqueda, **entonces** el sistema muestra *"El destinatario ingresado no existe o no se encuentra activo"*.

---

### Historia 3 — Envío de dinero escaneando un código QR del destinatario

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario de la billetera, quiero escanear el código QR de otro usuario, para transferirle dinero presencialmente sin escribir sus datos. |

**Criterios de aceptación**

1. **Dado** que el usuario escanea un QR válido de la aplicación, **cuando** la cámara lee el código, **entonces** el sistema autocompleta los datos del destinatario y solicita el monto a enviar.
2. **Dado** que el código QR es ilegible o no pertenece al sistema, ****Criterios de aceptación** (continuación)

1. **Dado** que el usuario escanea un QR válido de la aplicación, **cuando** la cámara lee el código, **entonces** el sistema autocompleta los datos del destinatario y solicita el monto a enviar.
2. **Dado** que el código QR es inválido o no pertenece a la red, **cuando** la cámara lee el código, **entonces** el sistema indica *"Código QR no reconocido"*.

---

### Historia 4 — Transferencia programada o recurrente

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario de la billetera, quiero programar una transferencia para una fecha futura, para asegurar el pago en una fecha determinada. |

**Criterios de aceptación**

1. **Dado** que el usuario selecciona una fecha futura y un destinatario válido, **cuando** programa la transferencia, **entonces** el sistema registra la orden en estado "Programada".
2. **Dado** que llega la fecha programada y el usuario no tiene saldo suficiente, **cuando** el proceso automático intenta transferir, **entonces** la operación se cancela y se notifica al usuario por push.

---

### Historia 5 — Envío de dinero con mensaje y comprobante compartible

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario de la billetera, quiero adjuntar un concepto/nota y compartir el comprobante por WhatsApp al finalizar el envío, para avisarle al destinatario. |

**Criterios de aceptación**

1. **Dado** que una transferencia resulta exitosa, **cuando** se muestra la pantalla de éxito, **entonces** el sistema permite presionar "Compartir comprobante" para enviarlo vía imagen/PDF a apps de mensajería.
2. **Dado** que el usuario no ingresa concepto, **cuando** procesa el pago, **entonces** el sistema asigna el concepto predeterminado "Varios".

---

## Parte B — Los caminos que no salen bien

**Historia elegida:** Historia 1 — Envío de dinero a un contacto de la agenda con saldo suficiente

| Pregunta | Qué hace el sistema | Quién decide (analista / negocio / técnica) |
|----------|----------------------|-----------------------------------------------|
| ¿Qué pasa si el saldo es insuficiente? | Muestra un mensaje de error claro en pantalla, impide la transferencia y sugiere cargar dinero en la cuenta. | **Negocio** |
| ¿Qué pasa si el destinatario no existe o está dado de baja? | Interrumpe la operación en el paso de validación, informa *"La cuenta de destino se encuentra inactiva"* y no permite avanzar al ingreso del monto. | **Analista** |
| ¿Qué pasa si el sistema descuenta el saldo y falla antes de acreditarlo del otro lado? | Realiza un rollback (reversión atómica de la transacción) para reintegrar el saldo inmediatamente y registra la falla en la auditoría. | **Técnica** |
| ¿Qué pasa si el usuario aprieta "Enviar" dos veces? | Deshabilita el botón tras el primer clic y genera un token único por transacción (idempotencia) para evitar transferencias duplicadas. | **Técnica** |
| ¿Qué pasa si se cae la conexión justo después de confirmar? | Revisa el estado de la transacción mediante un reintento asincrónico antes de reintentar, notificando al usuario por e-mail/push si se procesó o no. | **Técnica** |

---

## Parte C — Defensa

_Se hace oral, en el plenario. No se documenta en este archivo._