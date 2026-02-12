# Presupuesto por Fases y Entregables (Escenario Pesimista)
## Sistema de Pedidos: Tienda Fran

**Fecha:** 2026-02-09
**Moneda:** USD (o ARS al tipo de cambio acordado al momento de firma)
**Nota interna:** presupuesto de piso para cerrar primer cliente. Margen minimo, prioriza portfolio y relacion comercial.

---

## Resumen General

| Fase | USD Pesimista | USD Base | Descuento |
|---|---|---|---|
| Fase 0 - Discovery | Bonificado | 500 | -100% |
| Fase 1 - MVP Single-Store | 3,500 | 6,000 | -42% |
| Fase 1.5 - Mejoras operativas | 2,000 | 4,000 | -50% |
| Fase 2 - B2B Mayorista | 3,500 | 6,000 | -42% |
| **Total proyecto completo** | **9,000** | **16,500** | **-45%** |

---

## Fase 0 - Discovery (1-2 semanas)

**Inversion:** USD 0 (bonificado)
**Condicion:** se bonifica como gesto comercial por ser primer cliente. Se absorbe el costo internamente.

| # | Entregable | Incluido |
|---|---|---|
| 1 | Relevamiento funcional y operativo del local | Si |
| 2 | Definicion de reglas criticas (delivery, horarios, minimos, estados) | Si |
| 3 | Mapa de procesos actual y objetivo | Si |
| 4 | Prototipo UX del flujo principal | Si |
| 5 | Backlog priorizado | Si |
| 6 | Cronograma con hitos | Si |
| 7 | Presupuesto final cerrado | Si |

**Justificacion interna:** el Discovery gratis baja la barrera de entrada. Si el cliente ve el prototipo y el plan, es mucho mas probable que cierre F1. Es una inversion en confianza.

---

## Fase 1 - MVP Single-Store (6-8 semanas)

**Inversion:** USD 3,500

### Desglose por modulo

| Modulo | USD |
|---|---|
| Base de datos + backend + API | 1,500 |
| Frontend storefront (tienda online B2C) | 800 |
| Panel de administracion | 600 |
| Deploy + configuracion + capacitacion | 300 |
| QA funcional y ajustes | 300 |
| **Subtotal Fase 1** | **3,500** |

### Entregables (mismos que el presupuesto base)

| # | Entregable |
|---|---|
| 1 | Base de datos y migraciones |
| 2 | Backend/API funcional con validaciones |
| 3 | Tienda online mobile-first (catalogo, carrito, checkout) |
| 4 | Panel admin (pedidos, productos, categorias, configuracion) |
| 5 | Testing funcional end-to-end |
| 6 | Despliegue a produccion con dominio, SSL y backups |
| 7 | Capacitacion al personal (1 hora) |
| 8 | Guia breve de uso |
| 9 | 15 dias de garantia post-lanzamiento |

### Recortes vs presupuesto base

- Capacitacion reducida a 1 hora (en vez de 2)
- Garantia reducida a 15 dias (en vez de 30)
- Diseno UI minimo (funcional, sin pulir al detalle)
- Sin variantes de producto en F1 (se posterga a F1.5)

---

## Fase 1.5 - Mejoras Operativas (2-4 semanas)

**Inversion:** USD 2,000

### Desglose por modulo

| Modulo | USD |
|---|---|
| Integracion MercadoPago | 400 |
| Reportes basicos (ventas por dia, ticket promedio) | 500 |
| Notificaciones (email basico) | 400 |
| Ajustes de UX post-lanzamiento | 300 |
| Funcion "Reordenar" | 200 |
| Variantes de producto (postergadas de F1) | 200 |
| **Subtotal Fase 1.5** | **2,000** |

### Recortes vs presupuesto base

- Notificaciones solo email (sin push)
- Sin comanda/impresion operativa
- Reportes mas acotados

---

## Fase 2 - B2B Mayorista (4-6 semanas)

**Inversion:** USD 3,500

### Desglose por modulo

| Modulo | USD |
|---|---|
| Login cerrado y gestion de clientes mayoristas | 600 |
| Catalogo B2B con precios diferenciados | 900 |
| Listas de precio por cliente/rubro | 600 |
| Pedidos mayoristas con minimos y condiciones | 600 |
| Historial y recompra rapida | 400 |
| Entrega programada | 200 |
| Deploy y ajustes | 200 |
| **Subtotal Fase 2** | **3,500** |

---

## Costos Recurrentes Mensuales

| Concepto | USD/mes |
|---|---|
| Infraestructura (hosting, DB, backups) | 20 |
| Servicios (email transaccional) | 5 |
| Soporte y mantenimiento tecnico | 75 |
| **Total mensual estimado** | **100** |

**Nota:** el soporte a $75/mes es minimo (2-3 horas/mes). Si el cliente necesita mas, se cobra aparte.

---

## Esquema de Pagos

| Hito | % |
|---|---|
| Inicio de la fase | 40% |
| Entrega funcional completa | 40% |
| Salida a produccion | 20% |

**Simplificado a 3 hitos** (en vez de 4) para facilitar el cierre.

### Ejemplo aplicado a Fase 1 (USD 3,500)

| Hito | Monto USD |
|---|---|
| Inicio | 1,400 |
| Entrega funcional | 1,400 |
| Salida productiva | 700 |

---

## Condiciones

- Cada fase tiene alcance cerrado. Cambios de alcance se presupuestan aparte.
- Garantia de 15 dias por fase (correccion de errores, no funcionalidades nuevas).
- Soporte post-garantia con plan mensual.
- Si se contrata F1 + F1.5 juntas, se respeta el precio sin ajuste.

---

## Analisis Interno: Que Perdemos y Que Ganamos

### Que perdemos

| Concepto | Impacto |
|---|---|
| Margen de ganancia | Minimo o nulo en F1. Se trabaja casi a costo. |
| Tiempo invertido vs cobrado | Desbalance claro. Las horas reales superan lo cobrado. |
| Discovery gratis | Costo absorbido (~10-15 horas de trabajo no cobradas) |
| Garantia corta | Menos margen para ajustes post-lanzamiento |

### Que ganamos

| Concepto | Valor |
|---|---|
| Primer proyecto en portfolio | Referencia real con cliente real |
| Caso de estudio | Para mostrar a futuros clientes |
| Codebase reutilizable | El core se reutiliza en proximos proyectos similares |
| Relacion comercial | Si funciona, F1.5, F2 y mantenimiento mensual son recurrentes |
| Experiencia de equipo | Proceso completo de punta a punta (discovery -> produccion) |
| Posible marketplace | Si evoluciona a Fase 3, el negocio escala sin este cliente como dependencia |

### Linea roja (no bajar de aca)

- **F1 no menor a USD 3,000.** Por debajo se pierde plata seguro.
- **Mantenimiento mensual no menor a USD 75.** Si no, no se sostiene.
- **No regalar F1.5 ni F2.** Discovery se puede bonificar, el resto no.
- **No prometer propiedad total del codigo a este precio.** El core es nuestro.

---

## Comparativa Rapida

| Concepto | Base | Pesimista | Diferencia |
|---|---|---|---|
| Discovery | 500 | 0 | -500 |
| Fase 1 | 6,000 | 3,500 | -2,500 |
| Fase 1.5 | 4,000 | 2,000 | -2,000 |
| Fase 2 | 6,000 | 3,500 | -2,500 |
| **Total** | **16,500** | **9,000** | **-7,500** |
| Mensual | 160 | 100 | -60 |

---

*Documento de uso interno. NO enviar al cliente. Usar como referencia de piso absoluto en la negociacion.*
