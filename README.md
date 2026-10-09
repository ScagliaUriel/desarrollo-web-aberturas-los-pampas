# 🪟 Aberturas Los Pampas — Sistema de Gestión, Cotización y Ventas Online

[![Estado del Proyecto](https://img.shields.io/badge/Estado-Excelente-success)](#)
[![Evaluación Docente](https://img.shields.io/badge/Evaluaci%C3%B3n-63%2F63%20pts-blue)](#)
[![Licencia](https://img.shields.io/badge/Licencia-MIT-green)](#)

Sistema web de e-commerce, cotización dinámica a medida y gestión operativa en tiempo real para la fábrica y distribuidora **Aberturas Los Pampas**.

---

## 📑 Tabla de Contenidos
- [Descripción del Proyecto](#descripción-del-proyecto)
- [Estructura del Repositorio](#estructura-del-repositorio)
- [Prototipo Funcional Navegable](#prototipo-funcional-navegable)
- [Documentación del Sistema](#documentación-del-sistema)
- [Ingeniería de Software y Modelado](#ingeniería-de-software-y-modelado)
- [Integrantes del Equipo](#integrantes-del-equipo)

---

## 📸 Descripción del Proyecto

**Aberturas Los Pampas** es una plataforma web integral diseñada para solucionar la brecha entre el canal de venta digital y la operación técnica/logística de la empresa.

### Funcionalidades Clave:
1. **Catálogo y Búsqueda Facetada:** Filtrado por tipología (ventanas, puertas, paños fijos), material (aluminio, PVC, madera, chapa) y precio con sincronización de stock en tiempo real.
2. **Cotización de Aberturas a Medida:** Algoritmo dinámico para solicitar presupuestos personalizados (alto, ancho, tipo de vidrio, acabado) y carga de planos técnicos[cite: 30, 31].
3. **Checkout y Pagos Digitales:** Integración con la API de Mercado Pago (tarjetas, dinero en cuenta) y emisión automática de comprobantes[cite: 30, 31].
4. **Administración Operativa:** Control de inventario, registro de órdenes de compra a proveedores, logs de auditoría y agendamiento de turnos de instalación[cite: 30, 31].

---

## 📂 Estructura del Repositorio

```text
.
├── README.md                          # Presentación general del proyecto
├── DoR.md                             # Matriz y criterios de Definition of Ready
├── slicing.md                         # Slicing vertical y decisiones de arquitectura/negocio
├── integrantes.md                     # Nómina del equipo de desarrollo
├── RECURSOS.md                        # Guía de entorno de trabajo y comandos git
├── docs/
│   ├── requisitos.md                  # Requisitos Funcionales (RF) y No Funcionales (RNF)
│   ├── historias-de-usuario.md        # Historias de Usuario con escenarios BDD e INVEST
│   ├── casos-de-uso.md                # Especificación detallada de Casos de Uso (CU)
│   ├── er-modelo.md                   # Modelo ER y justificación de decisiones de diseño
│   ├── diseño-ui.md                   # Patrones de interfaz, accesibilidad WCAG y wireframes
│   ├── stakeholders.md                # Matriz e impacto de partes interesadas
│   └── Prototipo/                     # Prototipo HTML5/CSS3/JS navegable
│       ├── Prototipo funcional — Aberturas Los Pampas.html
│       └── Prototipo funcional — Aberturas Los Pampas.md
├── diagramas/
│   ├── casos-de-uso.puml              # Diagrama PlantUML general de Casos de Uso
│   ├── er.puml                        # Diagrama PlantUML Entidad-Relación
│   └── wireframes/                    # Wireframes SVG de maquetación de interfaz
│       ├── 01-home-catalogo.svg
│       └── 11-cotizacion-a-medida.svg
└── feedback/                          # Historial de devoluciones docentes
    ├── 2026-09-02.md
    ├── 2026-09-06.md
    ├── 2026-09-16.md
    ├── 2026-09-18.md
    ├── 2026-09-28.md
    └── 2026-09-30.md