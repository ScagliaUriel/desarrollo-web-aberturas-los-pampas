# [Abertura Los Pampas] — Grupo [N]

> Materia: Diseño de Sistemas Web — Analista Funcional de Sistemas
> Institución: Terciario Urquiza — Rosario
> Docente: Pedernera Pablo
> Cuatrimestre: 2.° 2026

## Integrantes

Ver [integrantes.md](./integrantes.md)

## Descripción del proyecto

El proyecto consiste en el análisis, diseño y desarrollo de una plataforma web para **Aberturas Los Pampas**, empresa dedicada a la comercialización de aberturas (portones, puertas y ventanas fabricadas en chapa, madera y aluminio), rejas de hierro para ventanas, cortinas enrollables y cortinas roller, tanto en presentaciones estandarizadas como a medida, complementadas con servicios de instalación y subcontratación.

Actualmente la empresa no tiene presencia en ningún canal de internet vigente, por lo que el sistema propuesto busca cubrir esa necesidad mediante:

- Un **catálogo online de productos**, con tipos de aberturas, características, especificaciones y precios.
- Integración con **Mercado Pago** para la gestión de cobros de las ventas.
- Vinculación con las **redes sociales** de la empresa (Facebook, Instagram, etc.), actualmente inexistentes.
- Gestión de **usuarios/clientes**, con acceso a datos clave para la venta, el envío y la instalación de materiales, y visibilidad de las ventas mensuales.
- Gestión de **proveedores**, con datos para facturación, generación de órdenes de compra con sus plazos de entrega, e historial de compras para análisis de los productos más vendidos.
- Gestión de **stock**, cargando las cantidades disponibles de cada material en el catálogo online y permitiendo la compra de productos sin stock sujeta a los plazos de entrega de los proveedores.

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

## Entregas

| Entrega | Descripción             | Fecha | Estado |
| ------- | ----------------------- | ----- | ------ |
| EP-01   | Presentación preliminar |       |        |
| EP-02   |                         |       |        |
| Final   | Versión definitiva      |       |        |

## Estructura del repositorio

```
/
├── README.md
├── integrantes.md
├── RECURSOS.md         ← leer antes de empezar: prerrequisitos, cheatsheet de git, recursos
├── DoR.md              ← Definition of Ready: checklist del equipo + autoevaluación de 3 HU propias
├── slicing.md          ← épica de la billetera partida en historias verticales (Partes A y B)
├── docs/
│   ├── requisitos.md
│   ├── historias-de-usuario.md
│   ├── casos-de-uso.md
│   ├── er-modelo.md
│   ├── diseño-ui.md
│   └── stakeholders.md
├── diagramas/
│   ├── casos-de-uso.puml
│   ├── er.puml
│   └── wireframes/
└── cuestionario/
```

## Instrucciones operativas

- Un integrante del grupo es responsable de subir los cambios al repositorio.
- Completar `integrantes.md` antes de la primera entrega.
- Mantener los archivos en la carpeta correspondiente según la estructura indicada.
- Los diagramas deben entregarse en formato PlantUML (`.puml`). Se pueden visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/).
