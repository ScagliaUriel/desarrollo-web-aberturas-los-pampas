# Stakeholders — Aberturas Los Pampas

Mapa de actores internos y externos del proyecto, identificando sus intereses, necesidades y el nivel de impacto de cada uno en la solución web.

## Mapa de Stakeholders

| Stakeholder | Tipo | Interés en el proyecto | Necesidades / Expectativas | Ejemplo concreto | Nivel de Impacto |
| ----------- | ---- | ----------------------- | --------------------------- | ---------------- | ---------------- |
| **Propietarios (Padre e Hijo)** | Interno | Automatizar la gestión del negocio y aumentar las ventas fuera del canal presencial. | Reportes consolidados de ventas, control total de usuarios y escalabilidad del negocio. | Monitorear el volumen de facturación mensual y habilitar nuevos canales de venta online. | **Alto:** Tienen el poder de decisión final, presupuestario y de aprobación sobre la arquitectura del proyecto. |
| **Personal de Ventas** | Interno | Consultar disponibilidad de productos y agilizar la atención a clientes en mostrador. | Interfaz simple y rápida para verificar stock disponible en tiempo real durante la atención. | Un vendedor consulta desde el mostrador si hay stock de una puerta de madera. | **Medio:** Usan el sistema diariamente para la operación comercial, pero no definen los requisitos ni el presupuesto. |
| **Personal de Depósito / Stock** | Interno | Mantener el inventario físico sincronizado con las ventas web. | Registrar entradas, salidas y recibir alertas automáticas de reposición de mercadería. | El encargado del depósito actualiza el ingreso de un lote de ventanas de aluminio. | **Medio:** Determinante para la precisión del stock físico y la logística, pero dependiente de las directivas administrativas. |
| **Clientes Minoristas** | Externo | Comprar aberturas de forma rápida, ver precios transparentes y pagar online. | Catálogo claro, medios de pago digitales e información sobre tiempos de entrega e instalación. | Un cliente particular compra una ventana estándar de chapa y paga mediante Mercado Pago. | **Alto:** Son los usuarios finales primarios que generan los ingresos directos del canal e-commerce B2C. |
| **Clientes Mayoristas (Constructoras/Arquitectos)** | Externo | Solicitar cotizaciones por volumen y consultar productos con especificaciones técnicas. | Atención personalizada, cotizaciones a medida y compras corporativas. | Una constructora solicita la cotización de 50 ventanas de aluminio para una obra. | **Alto:** Representan el mayor volumen financiero por transacción y la recurrencia comercial de la empresa. |
| **Proveedores de Aberturas** | Externo | Recibir órdenes de compra formalizadas con plazos claros de entrega. | Comunicación directa y previsibilidad en los pedidos de reposición. | Un proveedor de portones recibe una orden de compra automatizada desde el panel. | **Bajo:** Interactúan de manera indirecta únicamente a través de la recepción de órdenes de compra consolidadas. |
| **Técnicos Instaladores** | Externo | Contar con la información precisa de direcciones y especificaciones para la colocación. | Claridad en las fechas asignadas, medidas del producto y requerimientos del cliente. | Un instalador recibe la dirección y ficha técnica para colocar una cortina roller. | **Medio:** Su trabajo incide directamente en la satisfacción final del cliente y la reputación del servicio postventa. |
| **Mercado Pago** | Externo | Procesar las transacciones de pago con altos estándares de seguridad. | Integración estable mediante API y comunicación fluida de estados de pago. | Notificación automática de cobro aprobado hacia el sistema para liberar el pedido. | **Alto:** Es la pasarela crítica de procesamiento de cobros; su fallo interrumpe las ventas online. |
| **Proveedor de Internet (ISP / Claro)** | Externo | Mantener la conectividad a internet en el local comercial. | Cobro en fecha de abono y reporte de fallas de servicio. | Garantizar enlace de fibra óptica para que el panel de administración esté en línea. | **Bajo:** Provee la infraestructura base pero no interactúa directamente con el software desarrollado. |

---

## Equipo del proyecto

| Stakeholder | Rol | Interés en el proyecto | Nivel de Impacto |
| ----------- | --- | ----------------------- | ---------------- |
| **Grupo de desarrollo** | Analistas funcionales / desarrolladores (ver [integrantes.md](/integrantes.md)) | Relevar requisitos, diseñar y documentar la solución web. | **Alto:** Responsables directos del diseño, la codificación y la ejecución técnica del sistema. |
| **Docente Pedernera Pablo** | Docente de la materia Desarrollo de Sistemas Web | Evaluación y seguimiento de las entregas del trabajo práctico anual. | **Alto:** Define las rúbricas de evaluación, valida la arquitectura y otorga la aprobación de la materia. |