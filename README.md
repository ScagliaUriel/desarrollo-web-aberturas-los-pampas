# Aberturas Los Pampas

Sistema web para la gestión, cotización y venta online de aberturas y perfiles de aluminio, PVC y madera.

## Descripción del proyecto

Aberturas Los Pampas busca cerrar la brecha entre la venta digital y la operación comercial del negocio. La plataforma integra un catálogo público, cotizaciones a medida, checkout con pago digital, seguimiento del estado de pedidos y herramientas internas para stock, proveedores y gestión operativa.

El proyecto se desarrolla como un caso de estudio de diseño de sistemas web, con foco en requerimientos funcionales y no funcionales, historias de usuario, casos de uso, diagramas de entidad-relación, wireframes y prototipo navegable.

## Objetivos principales

- Facilitar la compra de productos estándar y personalizados desde un sitio web claro y responsive.
- Soportar la cotización a medida con dimensiones, materiales y resumen de estimación.
- Integrar un flujo de checkout con validación de stock y pago digital.
- Brindar herramientas internas para controlar inventario, compras a proveedores y seguimiento de pedidos.

## Caso de estudio

**Aberturas Los Pampas** es una empresa ubicada en la zona norte de Rosario, en la calle Huerta Grande 1985. Inició su actividad en el año 2012 como un proyecto familiar entre padre e hijo, impulsado por la falta de empleo de este último. Con algunos ahorros y la venta de bienes personales, comenzaron comprando mercadería para su comercialización, apoyándose en la experiencia previa del padre como representante de otra empresa de aberturas en la provincia de Santa Fe.

La empresa atiende tanto a consumidores minoristas como a mayoristas (ferreterías, corralones, constructoras, estudios de arquitectura y otros negocios del rubro).

**Infraestructura tecnológica actual:** dos computadoras de escritorio (ventas y stock), una notebook de uso del propietario, un televisor digital en recepción, un módem Wi-Fi de 100 Mbps (Claro) con alcance en todo el edificio, dos celulares de uso comercial, una línea fija, alarmas en local y galpón, conexión eléctrica trifásica, posnet y dos impresoras Wi-Fi.

**Problemática detectada:**

- **Ventas:** ausencia de presencia en internet y de una página web propia para comercializar los productos.
- **Redes:** falta de presencia en redes sociales y de vinculación con un catálogo digital.
- **Clientes:** no existe un sistema de usuarios que centralice datos de venta, envío e instalación.
- **Proveedores:** no hay un control sistematizado de datos de facturación, órdenes de compra ni historial de compras.
- **Stock:** no hay integración entre el control de stock y un canal de venta online.
- **Seguridad informática:** equipos desactualizados y sin mantenimiento regular, ausencia de red segura, uso indiscriminado de los dispositivos, celulares comerciales sin contraseña y personal sin capacitación en seguridad de la información.
- **Infraestructura eléctrica:** sin estabilizador de tensión ni correcta división de circuitos.

Este diagnóstico es la base sobre la que el equipo releva requisitos, define historias de usuario y diseña la solución web para la empresa.

## Documentación del sistema

- `docs/requisitos.md`: requisitos funcionales y no funcionales.
- `docs/historias-de-usuario.md`: historias de usuario con criterios de aceptación e INVEST.
- `docs/casos-de-uso.md`: especificación de actores, casos de uso y excepciones.
- `docs/er-modelo.md`: modelo entidad-relación y decisiones de diseño.
- `docs/diseño-ui.md`: patrones de diseño, accesibilidad y cobertura de wireframes.
- `docs/stakeholders.md`: análisis de stakeholders e impacto.
- `DoR.md`: checklist de Definition of Ready por historia.
- `slicing.md`: partición vertical de la épica y decisiones de negocio/arquitectura.

## Prototipo y wireframes

- `diagramas/wireframes/01-home-catalogo.svg`
- `diagramas/wireframes/02-ficha-producto.svg`
- `diagramas/wireframes/03-carrito.svg`
- `diagramas/wireframes/04-checkout-pago.svg`
- `diagramas/wireframes/05-cuenta-cliente.svg`
- `diagramas/wireframes/06-login-interno.svg`
- `diagramas/wireframes/07-gestion-productos-stock.svg`
- `diagramas/wireframes/08-gestion-proveedores.svg`
- `diagramas/wireframes/09-gestion-pedidos-ventas.svg`
- `diagramas/wireframes/10-reportes.svg`
- `diagramas/wireframes/11-cotizacion-a-medida.svg`

El prototipo navegable se encuentra en `docs/Prototipo/`.

## Estructura del repositorio

```text
.
├── README.md
├── DoR.md
├── slicing.md
├── integrantes.md
├── RECURSOS.md
├── docs/
│   ├── requisitos.md
│   ├── historias-de-usuario.md
│   ├── casos-de-uso.md
│   ├── er-modelo.md
│   ├── diseño-ui.md
│   ├── stakeholders.md
│   ├── index.html (acceso y redirección a GitHub Pages)
│   └── Prototipo/
│       ├── index.html
│       ├── styles.css
│       ├── app.js
│       ├── Prototipo funcional — Aberturas Los Pampas.html
│       └── Prototipo funcional — Aberturas Los Pampas.md
├── diagramas/
│   ├── casos-de-uso.puml
│   ├── er.puml
│   └── wireframes/
│       ├── 01-home-catalogo.svg
│       ├── 02-ficha-producto.svg
│       ├── 03-carrito.svg
│       ├── 04-checkout-pago.svg
│       ├── 05-cuenta-cliente.svg
│       ├── 06-login-interno.svg
│       ├── 07-gestion-productos-stock.svg
│       ├── 08-gestion-proveedores.svg
│       ├── 09-gestion-pedidos-ventas.svg
│       ├── 10-reportes.svg
│       └── 11-cotizacion-a-medida.svg
└── feedback/
    ├── 2026-09-02.md
    ├── 2026-09-06.md
    ├── 2026-09-16.md
    ├── 2026-09-18.md
    ├── 2026-09-28.md
    ├── 2026-09-30.md
    ├── 2026-10-09.md
    ├── 2026-10-14.md
    └── 2026-10-16.md
```

## Integrantes del equipo

- Máximo Manno
- Alan Grandi
- Román Peralta
- Uriel Scaglia

## Estado del proyecto

La entrega actual incluye la documentación funcional, validación del alcance, mockups y fundamentos de diseño del sistema. El repositorio se mantiene actualizado con la revisión docente y con la coherencia entre requisitos, historias, casos de uso y wireframes.