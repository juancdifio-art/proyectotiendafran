# Propuesta de Solución: Sistema de Pedidos - Tienda Fran
**Cliente:** Fran (Tienda Fran)  
**Fecha:** 2026-02-11  
**Preparado por:** Infinite Solutions (Rodrigo Aguinagalde & Juan)

---

## 1. Introducción y Diagnóstico
Tras nuestra reunión inicial, identificamos que **Tienda Fran** presenta la necesidad de optimizar su proceso de **gestión de pedidos y ventas online**. 

Actualmente, el manejo mediante **WhatsApp, llamadas telefónicas y atención en mostrador** genera desafíos en cuanto a eficiencia, trazabilidad y escalabilidad. Se pierden pedidos, no hay un sistema unificado de seguimiento, y la dependencia de plataformas como PedidosYa implica comisiones del 20-30% sobre cada venta.

La propuesta de **Infinite Solutions** busca digitalizar y automatizar estos flujos mediante una tienda online propia, eliminando intermediarios y reduciendo errores operativos.

---

## 2. Descripción de la Solución
Desarrollaremos un **Sistema de Gestión Web (Tienda Online + Panel de Administración)** a medida. La solución será:
* **Accesible:** Mobile-first, disponible desde cualquier celular o PC sin necesidad de descargar una app.
* **Escalable:** Preparada para crecer junto al negocio, con un segundo bloque B2B mayorista planificado.
* **Segura:** Con protocolos de autenticación (JWT, bcrypt), respaldo de datos y validaciones en backend.

---

## 3. Alcance del Proyecto (Funcionalidades)

El proyecto se divide en **dos bloques** con alcance cerrado y precio definido:

### Bloque 1: Discovery + MVP + Mejoras (USD 1,500)

#### Fase Discovery (Meses 1-2)
* [ ] Relevamiento funcional del local y su operación diaria.
* [ ] Definición de reglas de negocio (delivery, horarios, mínimos, zonas).
* [ ] Prototipo UX del flujo principal de compra.
* [ ] Backlog priorizado de desarrollo.

#### Módulo Tienda Online — Fase 1 MVP (Meses 2-6)
* [ ] Catálogo de productos organizado por categorías (Comidas, Helados, Mercadería, Alfajores, etc.).
* [ ] Carrito de compras con resumen y cálculo de costo de envío.
* [ ] Checkout simple: nombre, teléfono, dirección (si es delivery).
* [ ] Confirmación instantánea del pedido con número de seguimiento.
* [ ] Gestión de horarios de atención y cierre por día de la semana.
* [ ] Modo pausa: cerrar la tienda al instante ante cualquier necesidad.
* [ ] Métodos de entrega: retiro en local y/o envío a domicilio (costo fijo o por zona).

#### Módulo de Administración — Fase 1 MVP (Meses 2-6)
* [ ] Bandeja de pedidos en tiempo real con estados claros (Nuevo → En preparación → Listo → Enviado/Retirado → Cerrado).
* [ ] Gestión de productos: agregar, editar, pausar, cambiar precios.
* [ ] Gestión de categorías con orden configurable.
* [ ] Configuración del local: horarios, métodos de entrega, costos de envío, pedido mínimo.
* [ ] Deploy a producción con dominio propio y SSL.
* [ ] Capacitación al personal y guía de uso.

#### Mejoras — Fase 1.5 (Meses 7-10)
* [ ] Integración con Mercado Pago para pagos online.
* [ ] Reportes básicos (ventas por día, ticket promedio).
* [ ] Notificaciones por email al cliente.
* [ ] Función "Reordenar" pedido anterior.
* [ ] Ajustes de UX basados en uso real post-lanzamiento.

### Bloque 2: Portal B2B Mayorista (USD 1,000) — Opcional

#### Módulo B2B (Meses 11-16)
* [ ] Portal B2B con acceso restringido (solo clientes mayoristas aprobados).
* [ ] Catálogo mayorista con presentaciones especiales (caja, bulto, docena).
* [ ] Precios diferenciados por cliente o rubro.
* [ ] Pedidos con mínimos de compra y condiciones especiales.
* [ ] Historial de pedidos y función "repetir pedido".
* [ ] Entrega programada con selección de fecha y hora.

---

## 4. Cronograma de Trabajo

Estimamos un tiempo total de desarrollo de **8 meses**, divididos de la siguiente manera:

### Fase 0 — Discovery (Mes 1)

| Mes | Actividad principal |
|---|---|
| Mes 1 | Discovery: relevamiento, reglas de negocio, prototipo UX, backlog priorizado |

### Fase 1 — MVP Tienda Online (Meses 2-5)

| Mes | Actividad principal |
|---|---|
| Mes 2 | Base de datos, autenticación, catálogo y productos |
| Mes 3 | Carrito, checkout, creación de pedidos |
| Mes 4 | Bandeja admin, estados de pedido, configuración del local |
| **Mes 5** | **QA, ajustes, deploy → TIENDA EN PRODUCCIÓN** |

> **Hito clave — Mes 5:** la tienda está en producción y recibiendo pedidos reales. A partir de este momento se activa la comisión del 2% sobre ventas.

### Fase 1.5 — Mejoras post-lanzamiento (Meses 6-7)

| Mes | Actividad principal |
|---|---|
| Mes 6 | Estabilización + integración Mercado Pago + reportes básicos |
| Mes 7 | Notificaciones por email + función reordenar + ajustes UX |

### Fase 2 — Portal B2B Mayorista (Mes 8)

| Mes | Actividad principal |
|---|---|
| Mes 8 | Portal B2B: login cerrado, catálogo mayorista, precios diferenciados, pedidos con mínimos, historial, recompra, entrega programada, QA y deploy |

---

## 5. Inversión y Forma de Pago

La inversión total por el desarrollo integral descrito es de:

### **Total: USD 2,500 en 12 cuotas mensuales de ~USD 209**

**Moneda:** USD pagaderos en ARS al tipo de cambio del día de pago.

### Plan de pagos — Desarrollo

| Cuota | Período | USD/mes |
|---|---|---|
| 1 a 12 | Mes 1 al 12 | ~209 |
| **Total** | | **2,500** |

El desarrollo se completa en aproximadamente 8 meses. Las cuotas restantes (meses 9 a 12) se continúan abonando como parte del plan de pagos acordado.

### Comisión sobre ventas (desde la salida a producción)

* **Porcentaje:** 2% sobre ventas brutas generadas por la tienda.
* **Desde cuándo:** Desde el momento en que la tienda sale a producción (estimado Mes 5).
* **Hasta cuándo:** Permanente mientras se use la plataforma.
* **Base de cálculo:** Sumatoria del total de pedidos en estado "Cerrado" en el mes.
* **No incluye:** Pedidos cancelados, costo de envío, impuestos.
* **Auditoría:** Reporte automático generado desde el panel admin.
* **Cobro:** Junto con la cuota o mantenimiento del mes siguiente.

### Post-desarrollo: Mantenimiento (a partir del Mes 13)

| Concepto | Monto |
|---|---|
| Soporte y mantenimiento mensual | USD 100/mes |
| Comisión sobre ventas brutas | 2% |
| Infraestructura (hosting, DB, backups) | Incluido |

El mantenimiento incluye: hosting, backups, corrección de bugs, actualizaciones de seguridad y 2-3 horas de soporte/ajustes menores por mes. Cambios mayores se presupuestan aparte.

---

## 6. Consideraciones Finales (Scope Freeze)

| Concepto | Detalle |
|---|---|
| **Vencimiento** | Día 10 de cada mes (o fecha a acordar) |
| **Mora** | Después de 15 días de atraso, se pausa el desarrollo hasta regularizar |
| **Cancelación anticipada** | Si cancela antes de la salida a producción, paga saldo restante de las 12 cuotas como penalidad |
| **Cambios de alcance** | Se presupuestan aparte. Las cuotas cubren el alcance definido en esta propuesta |
| **Propiedad de datos** | Todos los datos del cliente (pedidos, clientes, catálogo) son suyos y exportables |
| **Propiedad del código** | El core reutilizable es del equipo desarrollador |
| **Garantía** | Incluida durante el período de cuotas. Post-cuotas = plan de mantenimiento |

* Esta propuesta incluye exclusivamente las funcionalidades detalladas en el punto 3.
* Cualquier funcionalidad adicional solicitada durante el desarrollo será evaluada y presupuestada como un anexo aparte para no afectar los plazos de entrega del proyecto original.

### Qué NO incluye esta propuesta

* Marketplace con otros comercios.
* Facturación electrónica / AFIP.
* Seguimiento del repartidor en mapa.
* App nativa para celular (la tienda funciona desde el navegador, sin descargas).
* Integración con sistemas contables.

---

**Infinite Solutions** *Transformando procesos en software eficiente.*