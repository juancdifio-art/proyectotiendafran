# Presupuesto con Plan de Pagos Mensual
## Sistema de Pedidos: Tienda Fran

**Fecha:** 2026-02-09
**Moneda:** USD (pagaderos en ARS al tipo de cambio del dia de pago)

---

## Estructura

| Bloque | Alcance | Precio USD | Cuotas | Cuota USD/mes |
|---|---|---|---|---|
| Bloque 1 | Discovery + F1 + F1.5 | 1,500 | 10 | 150 |
| Bloque 2 | F2 - B2B Mayorista | 1,000 | 6 | ~167 |
| **Total** | **Proyecto completo** | **2,500** | **16 meses** | — |

**Ademas:** comision del 2-3% sobre ventas brutas generadas por la tienda, desde el lanzamiento (mes 6).

---

## Bloque 1: Discovery + MVP + Mejoras (USD 1,500)

### Plan de pagos: 10 cuotas de USD 150

| Cuota | Mes | USD | Actividad principal |
|---|---|---|---|
| 1 | Mes 1 | 150 | Discovery: relevamiento, reglas, prototipo |
| 2 | Mes 2 | 150 | Discovery cierre + inicio desarrollo (DB, auth) |
| 3 | Mes 3 | 150 | Catalogo, productos, CRUD admin |
| 4 | Mes 4 | 150 | Carrito, checkout, creacion de pedidos |
| 5 | Mes 5 | 150 | Bandeja admin, estados, config del local |
| 6 | Mes 6 | 150 | QA, ajustes, deploy, lanzamiento |
| 7 | Mes 7 | 150 | Estabilizacion post-lanzamiento + ajustes UX |
| 8 | Mes 8 | 150 | MercadoPago + reportes basicos |
| 9 | Mes 9 | 150 | Notificaciones + reordenar |
| 10 | Mes 10 | 150 | Ajustes finales F1.5, cierre bloque |
| **Total** | | **1,500** | |

### Que incluye el Bloque 1

**Discovery (meses 1-2):**
- Relevamiento funcional del local
- Definicion de reglas (delivery, horarios, minimos)
- Prototipo UX del flujo principal
- Backlog priorizado

**MVP - Fase 1 (meses 2-6):**
- Tienda online mobile-first (catalogo, carrito, checkout)
- Panel admin (pedidos, productos, categorias, configuracion)
- Gestion de horarios y pausa manual
- Envio fijo o por zona
- Deploy a produccion con dominio y SSL
- Capacitacion al personal
- Guia de uso

**Mejoras - Fase 1.5 (meses 7-10):**
- Integracion MercadoPago
- Reportes basicos (ventas por dia, ticket promedio)
- Notificaciones por email
- Funcion "Reordenar"
- Ajustes de UX basados en uso real

### Hito de entrega clave

**Mes 6: la tienda esta en produccion y recibiendo pedidos reales.**

---

## Bloque 2: B2B Mayorista (USD 1,000)

### Plan de pagos: 6 cuotas de ~USD 167

| Cuota | Mes | USD | Actividad principal |
|---|---|---|---|
| 11 | Mes 11 | 167 | Login cerrado + gestion clientes mayoristas |
| 12 | Mes 12 | 167 | Catalogo B2B + precios diferenciados |
| 13 | Mes 13 | 167 | Listas de precio por cliente/rubro |
| 14 | Mes 14 | 167 | Pedidos mayoristas con minimos |
| 15 | Mes 15 | 166 | Historial + recompra + entrega programada |
| 16 | Mes 16 | 166 | QA, deploy, capacitacion B2B |
| **Total** | | **1,000** | |

### Que incluye el Bloque 2

- Portal B2B con acceso restringido (solo clientes aprobados)
- Catalogo mayorista con presentaciones (caja, bulto, docena)
- Precios diferenciados por cliente o rubro
- Pedidos con minimos de compra y condiciones
- Historial de pedidos y "repetir pedido"
- Entrega programada (seleccion fecha/hora)

---

## Post-desarrollo: Mantenimiento + Comision (a partir del mes 17)

| Concepto | Monto |
|---|---|
| Soporte y mantenimiento | USD 75 - 100/mes |
| Comision sobre ventas brutas | 2-3% |
| Infraestructura (hosting, DB, backups) | incluido |

El mantenimiento incluye:
- Hosting y backups
- Correccion de bugs
- Actualizaciones de seguridad
- 2-3 horas de soporte/ajustes menores por mes
- Cambios mayores se presupuestan aparte

La comision se cobra desde el mes 6 (lanzamiento) de forma permanente.

---

## Flujo de Pagos Completo (16 meses + mantenimiento)

```
MES   CONCEPTO                              USD         COMISION
 1    Cuota 1/10 - Bloque 1                 150         -
 2    Cuota 2/10                             150         -
 3    Cuota 3/10                             150         -
 4    Cuota 4/10                             150         -
 5    Cuota 5/10                             150         -
 6    Cuota 6/10  >>> TIENDA EN PRODUCCION   150         + 2-3% ventas
 7    Cuota 7/10                             150         + 2-3% ventas
 8    Cuota 8/10                             150         + 2-3% ventas
 9    Cuota 9/10                             150         + 2-3% ventas
10    Cuota 10/10 - Cierra Bloque 1          150         + 2-3% ventas
11    Cuota 1/6  - Bloque 2 (B2B)           167         + 2-3% ventas
12    Cuota 2/6                              167         + 2-3% ventas
13    Cuota 3/6                              167         + 2-3% ventas
14    Cuota 4/6                              167         + 2-3% ventas
15    Cuota 5/6                              166         + 2-3% ventas
16    Cuota 6/6  - Cierra Bloque 2          166         + 2-3% ventas
17+   Mantenimiento mensual               75-100        + 2-3% ventas
```

**Total desarrollo: USD 2,500 en 16 cuotas + 2-3% de comision sobre ventas desde el mes 6.**

### Proyeccion de comision (desde mes 6 en adelante)

| Ventas brutas mensuales | Comision 2% | Comision 3% |
|---|---|---|
| USD 300 | 6 | 9 |
| USD 500 | 10 | 15 |
| USD 1,000 | 20 | 30 |
| USD 2,000 | 40 | 60 |
| USD 5,000 | 100 | 150 |
| USD 10,000 | 200 | 300 |

---

## Como Presentarlo al Cliente

> "Te proponemos esto: todo el desarrollo de tu tienda online — catalogo, pedidos, panel, delivery, todo — por **150 dolares por mes durante 10 meses**.
>
> A los 6 meses ya tenes la tienda funcionando y recibiendo pedidos. Los 4 meses siguientes le sumamos pagos online, reportes y mejoras.
>
> Si despues queres el canal mayorista para la distribuidora, son 6 cuotas mas de 167 dolares.
>
> Cuando la tienda este funcionando, nos llevamos un 3% de lo que vendas por ahi. Si en un mes vendes 500 dolares, son 15 dolares para nosotros. Compara eso con el 25% que te cobra PedidosYa.
>
> Despues del desarrollo, el mantenimiento son 75-100 dolares por mes mas el mismo 3%.
>
> **Son 150 dolares por mes para arrancar. Menos que una publicidad de Instagram.**"

---

## Condiciones Importantes

| Concepto | Detalle |
|---|---|
| **Moneda** | USD pagaderos en ARS al tipo de cambio del dia de pago |
| **Vencimiento** | Dia 10 de cada mes (o fecha a acordar) |
| **Mora** | Despues de 15 dias de atraso, se pausa el desarrollo hasta regularizar |
| **Cancelacion anticipada** | Si cancela antes del mes 6, paga saldo restante del Bloque 1 como penalidad |
| **Bloque 2 es opcional** | El cliente puede decidir no hacer B2B. Solo paga Bloque 1. |
| **Cambios de alcance** | Se presupuestan aparte. Las cuotas cubren el alcance definido. |
| **Propiedad de datos** | Todos los datos del cliente (pedidos, clientes, catalogo) son suyos |
| **Propiedad del codigo** | El core reutilizable es del equipo desarrollador |
| **Garantia** | Incluida durante el periodo de cuotas. Post-cuotas = mantenimiento. |

---

## Definicion de Comision sobre Ventas

| Concepto | Detalle |
|---|---|
| **Porcentaje** | 2-3% sobre ventas brutas (negociar 3%) |
| **Desde cuando** | Mes 6 (lanzamiento de la tienda) |
| **Hasta cuando** | Permanente mientras use la plataforma |
| **Base de calculo** | Sumatoria de `total` de pedidos en estado "Cerrado" en el mes |
| **No incluye** | Pedidos cancelados, costo de envio, impuestos |
| **Como se audita** | Reporte automatico generado desde el panel admin |
| **Cuando se cobra** | Junto con la cuota/mantenimiento del mes siguiente |

### Negociacion del porcentaje

- **Arrancar pidiendo 3%.** El argumento es simple: PedidosYa cobra 25%, Rappi 30%. Un 3% es nada.
- **Piso aceptable: 2%.** Si el cliente negocia mucho, no bajar de 2%.
- **No aceptar comision solo sobre "ventas nuevas" o "ventas que no hubiera tenido".** Es imposible de medir y genera conflictos. Es sobre todas las ventas por la tienda, punto.

---

## Comparativa con Modelos Anteriores

| Concepto | Base | Pesimista | Cuota+Comision | Plan de Pagos |
|---|---|---|---|---|
| Total desarrollo | USD 16,500 | USD 9,000 | USD 1,500 | USD 2,500 |
| Pago mensual max | Variable | Variable | ARS 200,000 | USD 167 |
| Duracion de pagos | Por hitos | Por hitos | 12 meses | 16 meses |
| Facil de cerrar | Dificil | Media | Muy facil | Muy facil |
| Ingreso mensual | Irregular | Irregular | Fijo | Fijo + variable |
| Comision | No | No | 2-3% | 2-3% |

---

*Documento de uso interno. Adaptar la seccion "Como presentarlo" para la reunion con el cliente.*
