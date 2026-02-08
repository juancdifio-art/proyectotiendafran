# Proyecto Completo para Analisis y Toma de Decisiones
## Sistema de Pedidos y Gestion Comercial (Consolidado byme + main)

**Fecha:** 2026-02-07  
**Estado:** borrador consolidado para estudio interno y preparacion comercial

## Base documental consolidada
### Documentos byme
- `proyectotiendafran-byme/chat-1.md`
- `proyectotiendafran-byme/chat-2-md`
- `proyectotiendafran-byme/comparativa-byme-vs-main.md`
- `proyectotiendafran-byme/propuesta-consolidada-martes.md`
- `proyectotiendafran-byme/propuesta-astro.md`

### Documentos main (companero)
- `proyectotiendafran-main/docs de inicio/beluga.md`
- `proyectotiendafran-main/docs de inicio/chatgpt52.md`
- `proyectotiendafran-main/docs de inicio/geminiflash3.md`
- `proyectotiendafran-main/docs de inicio/glm46.md`
- `proyectotiendafran-main/docs de inicio/propuesta-unificada.md`

---

## 1) Objetivo de este documento
Concentrar en un solo plan toda la informacion actual para decidir:
- estrategia de producto por fases
- arquitectura de Fase 1
- presupuesto por escenarios
- modelo comercial de cierre
- riesgos y decisiones pendientes antes de firmar

---

## 2) Contexto de negocio unificado
- Negocio hibrido: local minorista + linea mayorista (alfajores/distribucion).
- Operacion actual con canales manuales y baja trazabilidad.
- Necesidad de ordenar pedidos, stock y estados de punta a punta.
- Vision: iniciar con tienda propia y escalar (B2B, luego multi-comercio si hay traccion).
- Existe software legacy (DataLife), no usado como nucleo operativo.

---

## 3) Aportes incorporados desde `main` (companero)
1. Mensaje de valor comercial claro:
   - "Verdad unica del stock"
   - eficiencia mayorista (menos WhatsApp)
   - propiedad de datos y menor dependencia de comisiones externas
2. Estructura comercial robusta:
   - Discovery pago/descontable
   - hitos de cobro
   - garantia post salida
   - costos recurrentes explicitados
3. Exclusiones bien definidas para evitar malentendidos:
   - AFIP/fiscal
   - hardware POS especifico
   - contabilidad completa
   - marketplace multi-local
4. Escenarios de presupuesto por paquetes (MVP / Estandar / Premium).
5. Alternativa para reducir costo:
   - canal B2B como web responsive en lugar de app nativa en etapa inicial.

---

## 4) Problema a resolver y propuesta de valor
### Problemas actuales
- pedidos dispersos en WhatsApp/llamadas
- errores operativos y menor trazabilidad
- dificultad para medir estado de pedidos y ventas
- baja base para escalar digitalmente

### Propuesta de valor consolidada
- unificar operacion en un sistema central
- habilitar canal digital propio (sin comisiones por pedido)
- separar correctamente B2C y B2B en fases
- construir base tecnica escalable sin sobreprometer en Fase 1

---

## 5) Estrategia recomendada por fases (consenso)
Principio rector: **primero vender y operar bien, despues escalar**.

1. Fase 0: Discovery (alcance y reglas cerradas)
2. Fase 1: MVP single-store
3. Fase 1.5: mejoras operativas
4. Fase 2: B2B mayorista real
5. Fase 3: multi-comercio (solo si negocio lo justifica)

---

## 6) Alcance detallado por fase
## Fase 0 - Discovery (1-2 semanas)
**Objetivo:** bajar incertidumbre comercial y tecnica.

**Entregables:**
- documento de requerimientos
- reglas de negocio cerradas
- prototipo UX de flujo principal
- backlog priorizado
- cronograma y presupuesto final por fases

**Modelo recomendado:** fase paga y descontable del proyecto total.

## Fase 1 - MVP Single-Store (6-8 semanas)
**Incluye (B2C + Admin):**
- catalogo por categorias
- carrito + checkout
- retiro y envio local
- confirmacion de pedido con ID
- panel admin con estados de pedido
- CRUD de productos/categorias
- horarios y pausa de pedidos

**Fuera de alcance en F1:**
- marketplace multi-comercio
- tracking de repartidor en mapa
- AFIP y contabilidad completa
- integracion profunda con DataLife

## Fase 1.5 - Operacion (2-4 semanas)
- MercadoPago
- comanda/impresion
- reportes base
- mejoras por feedback real

## Fase 2 - B2B Mayorista (4-6 semanas)
- login cerrado de comercios
- listas de precio por cliente
- minimos/condiciones
- repeticion de pedido
- entrega programada
- opcion cuenta corriente (modulo adicional)

**Variante de costo:** iniciar B2B como web responsive antes de app nativa.

## Fase 3 - Multi-comercio (a evaluar)
- onboarding de comercios
- comisiones y liquidaciones
- soporte/reclamos centralizados
- administracion multi-store

---

## 7) Requisitos funcionales clave de Fase 1
### Cliente final
- explorar catalogo
- gestionar carrito
- checkout simple
- elegir retiro o envio
- recibir confirmacion con ID

### Admin local
- autenticacion segura
- bandeja de pedidos y cambios de estado
- motivo de cancelacion
- gestion de productos
- configuracion de horarios y pausa

### Flujo de estados
`Nuevo -> En preparacion -> Listo -> Enviado/Retirado -> Cerrado`

Flujo alternativo: `Cancelado`.

---

## 8) Requisitos no funcionales
- experiencia mobile-first
- alta performance de storefront
- validacion server-side de totales/precios
- logs de acciones criticas
- modelo con `store_id` desde inicio
- backups y monitoreo basico en produccion

---

## 9) Arquitectura: opciones para decidir
## Opcion A - Astro + React Islands + API Node/Express separada
**Pros:** performance/SEO, JS minimo, API reusable.

**Contras:** mas complejidad operativa inicial (2 despliegues, auth/CORS).

## Opcion B - Next.js Fullstack
**Pros:** menor complejidad inicial, velocidad de entrega MVP.

**Contras:** menor separacion explicita de capas desde el inicio.

## Decision practica sugerida
- Si priorizas velocidad y simplicidad: Opcion B.
- Si priorizas storefront ultra liviano y API separada desde el dia 1: Opcion A.

---

## 10) Matriz rapida de decision tecnica
| Criterio | Peso | Opcion A | Opcion B |
|---|---:|---:|---:|
| Time-to-market | 5 | 3 | 5 |
| Simplicidad operativa | 4 | 3 | 5 |
| Performance storefront | 4 | 5 | 4 |
| Reuso API futuro | 3 | 5 | 4 |
| Curva del equipo | 4 | 4 | 5 |
| **Total ponderado** | - | **70** | **86** |

Interpretacion: para Fase 1 acotada, hoy favorece Opcion B. Opcion A gana si la prioridad maxima es performance/SEO + separacion de backend.

---

## 11) Modelo de datos minimo sugerido
- `stores`
- `users`
- `categories`
- `products`
- `orders`
- `order_items` (snapshot de precio/nombre)
- `order_status_history`
- `store_settings`

**Nota de `main` incorporada:** para evolucion B2B sumar luego entidades de listas de precio, condiciones comerciales y cuenta corriente.

---

## 12) API minima sugerida
### Publica
- `GET /catalog`
- `GET /products/:id`
- `POST /orders`

### Admin
- `POST /auth/admin/login`
- `GET /admin/orders`
- `PATCH /admin/orders/:id/status`
- `GET/POST/PATCH /admin/products`
- `PATCH /admin/store/settings`

Regla no negociable: backend recalcula y valida totales/precios.

---

## 13) Entregables formales (fusion byme + main)
- documento de requerimientos y flujo de negocio
- prototipo UX/UI (pantallas clave)
- backend/API funcional
- panel admin operativo
- frontend cliente operativo
- testing funcional + correcciones
- despliegue a produccion
- capacitacion inicial y guia breve
- soporte post salida (periodo acordado)

---

## 14) Cronograma de referencia
### Ruta acotada (Discovery + F1)
- 1-2 semanas: Discovery
- 6-8 semanas: MVP
- 1 semana: salida y ajuste inicial

### Ruta integral (modelo `main`)
- 14-18 semanas incluyendo UX/UI extensa, mejoras, QA ampliado y salida formal.

---

## 15) Presupuesto por escenarios
## Escenario A - Entrada controlada (recomendado para cerrar)
- Discovery + F1
- USD 6,000 - 10,000

## Escenario B - Operacion consolidada
- Discovery + F1 + F1.5
- USD 10,000 - 16,000

## Escenario C - Expansion B2B
- Discovery + F1 + F1.5 + F2
- USD 16,000 - 26,000

## Referencia alternativa `main` (escenarios amplios)
- MVP Operativo: USD 8,000 - 15,000
- Estandar: USD 15,000 - 25,000
- Premium: USD 25,000 - 40,000+

**Uso recomendado:** tomar como bandas de negociacion y cerrar precio final luego de Discovery.

### Costos recurrentes estimados
- infraestructura: USD 30 - 120 / mes
- soporte: USD 120 - 350 / mes
- rango ampliado segun carga: hasta USD 380 / mes

---

## 16) Modelo comercial recomendado
- modalidad por hitos
- anticipo: 30%
- esquema: 30% inicio + 30% avance aprobado + 30% entrega + 10% salida
- garantia: 30 dias de correccion de errores
- cambios de alcance: adicionales formales
- Discovery: pago y descontable (si se contrata desarrollo completo)

---

## 17) Propiedad intelectual y modelo de licenciamiento (clave)
### Objetivo comercial
Permitir una entrada economica baja para el cliente sin perder la posibilidad de escalar a plataforma propia de ustedes.

### Esquema recomendado (para ticket inicial bajo)
- El cliente es dueno de:
  - su marca, dominio y contenido
  - sus datos operativos (clientes, pedidos, catalogo)
  - su configuracion especifica del negocio
- Ustedes conservan:
  - propiedad del core reutilizable (codigo base, arquitectura, componentes comunes)
  - derecho a reutilizar ese core en otros clientes/proyectos
  - derecho de operar la futura capa marketplace

### Derechos de uso para el cliente
- Licencia de uso del sistema dedicado para su operacion diaria.
- Continuidad operativa sujeta a mantenimiento/acuerdo de servicio.
- Exportacion de datos del cliente garantizada en formato acordado.

### Escalado a marketplace
- Si evoluciona a multi-comercio, la plataforma se opera bajo titularidad o control mayoritario de ustedes.
- El cliente fundador mantiene beneficio preferencial acordado:
  - comision reducida o bonificada por periodo inicial
  - prioridad comercial/operativa como comercio ancla

### Cuando hablarlo con el cliente
1. En Discovery: presentar el esquema de propiedad/licencia en forma preliminar.
2. En propuesta economica final: incluir anexo corto de \"propiedad intelectual y uso\".
3. Antes del anticipo: firmar clausulas claras en contrato.

### Que evitar
- No dejar este tema para despues de cerrar precio.
- No prometer \"propiedad total del software\" con ticket de implementacion bajo.

---

## 18) Exclusiones explicitas (evitar malentendidos)
- AFIP/facturacion electronica (salvo modulo adicional)
- impresoras fiscales o hardware POS especifico (salvo relevamiento)
- sistema contable completo
- marketplace multi-local en Fase 1
- integraciones ERP externas no planificadas

---

## 19) Riesgos y mitigacion
| Riesgo | Impacto | Mitigacion |
|---|---|---|
| Sobrealcance en F1 | atrasos/costo | recorte estricto del MVP |
| Reglas de stock ambiguas | errores operativos | taller obligatorio en Discovery |
| Cambios continuos de alcance | deriva de proyecto | backlog firmado por fase |
| Integraciones fiscales tardias | alta complejidad | tratar como modulo aparte |
| Arquitectura muy compleja en F1 | menor velocidad | priorizar simplicidad operativa |
| Confusion sobre propiedad del software | conflicto comercial/legal | definir licencia y titularidad desde Discovery |

---

## 20) Decisiones pendientes para reunion interna
1. Arquitectura F1: Opcion A (Astro+API) u Opcion B (Next fullstack).
2. Checkout invitado vs cuenta obligatoria.
3. Pago inicial: efectivo/transferencia o MercadoPago desde F1.
4. Delivery: fijo, zona o radio.
5. Horarios: inmediato vs programado.
6. B2B en F1: solo consulta o micro flujo.
7. Nivel minimo de reportes para salida.
8. Politica de soporte mensual.
9. Modelo de licencia exacto para este cliente (uso, permanencia, salida de datos).
10. Beneficio fundador si entra como primer comercio de futura plataforma.

---

## 21) Criterios Go/No-Go de lanzamiento
- cliente crea pedido completo (retiro y envio)
- admin procesa pedido de Nuevo a Cerrado
- horarios/pausa afectan checkout correctamente
- backend valida totales y precios
- flujo probado en mobile y desktop
- monitoreo y backups activos

---

## 22) Recomendacion final para tomar decision
1. Ejecutar Discovery corto y pago.
2. Cerrar alcance de F1 por escrito antes de desarrollar.
3. Lanzar una F1 acotada y estable.
4. Escalar a F1.5 y F2 solo con datos reales de uso.

Mensaje de cierre sugerido al cliente:
"Primero ordenamos ventas online y operacion del local. Luego escalamos mayorista y automatizaciones con base real, sin promesas vacias."

