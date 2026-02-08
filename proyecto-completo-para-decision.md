# Proyecto Completo para Analisis y Toma de Decisiones
## Sistema de Pedidos y Gestion Comercial (Local + Evolucion B2B)

**Fecha:** 2026-02-07  
**Estado:** borrador consolidado para estudio interno  
**Base documental:** `chat-1.md`, `chat-2-md`, `comparativa-byme-vs-main.md`, `propuesta-consolidada-martes.md`, `propuesta-astro.md`

---

## 1) Objetivo de este documento
Unificar toda la informacion actual en un solo plan ejecutable para decidir:
- que construir primero
- con que arquitectura
- cuanto cuesta cada etapa
- que riesgos aceptar y como mitigarlos

Este documento esta pensado para preparacion de propuesta comercial y para decision tecnica interna.

---

## 2) Contexto de negocio (resumen)
- El cliente tiene un local con venta minorista: comidas preparadas, helados, mercaderia, alfajores.
- Tambien existe un negocio mayorista de alfajores (distribuidora/fabrica familiar).
- Hoy la operacion digital no esta ordenada y depende mucho de canales manuales.
- Vision del cliente: comenzar como tienda propia y, a futuro, escalar a algo tipo marketplace local.
- Existe software legacy (DataLife o similar), pero no es eje de operacion actual.

---

## 3) Problema a resolver y valor esperado
### Problemas actuales
- pedidos por WhatsApp/llamadas sin trazabilidad clara
- riesgo de errores de preparacion y entrega
- baja visibilidad de estado de pedidos
- dificultad para escalar sin proceso digital

### Valor del proyecto
- canal digital propio sin comisiones de terceros por venta
- operacion ordenada por estados de pedido
- base de datos propia de clientes y ventas
- base tecnica para sumar B2B y luego marketplace

---

## 4) Estrategia recomendada (la decision mas importante)
No iniciar con marketplace completo.

Secuencia recomendada:
1. Discovery (cerrar reglas y alcance)
2. Fase 1 MVP single-store (vender y operar bien)
3. Fase 1.5 mejoras operativas
4. Fase 2 B2B mayorista
5. Fase 3 marketplace (solo con traccion validada)

Principio: validar negocio y operacion antes de subir complejidad estructural.

---

## 5) Alcance por fases y entregables
## Fase 0 - Discovery (1-2 semanas)
**Objetivo:** bajar incertidumbre y congelar alcance MVP.

**Entregables:**
- mapa de procesos actual y objetivo
- reglas de negocio cerradas (delivery, horarios, minimos, datos obligatorios)
- prototipo de flujo clave
- backlog priorizado
- estimacion final por fase y plan de hitos

## Fase 1 - MVP Single-Store (6-8 semanas)
**Objetivo:** operar pedidos online de un solo local de punta a punta.

**Incluye:**
- catalogo por categorias
- carrito + checkout
- retiro y envio local
- confirmacion de pedido con ID
- panel admin para gestionar pedidos y estados
- CRUD de productos/categorias
- horarios y pausa de pedidos

**No incluye:**
- marketplace multi-comercio
- tracking de repartidores en mapa
- integracion AFIP/contable
- integracion profunda con software legacy

## Fase 1.5 - Operacion (2-4 semanas)
**Incluye:**
- MercadoPago
- comanda/impresion (si aplica)
- reportes base (ventas por dia, producto, ticket promedio)
- mejoras UX/performance por feedback real

## Fase 2 - B2B Mayorista (4-6 semanas)
**Incluye:**
- login cerrado para clientes mayoristas
- listas de precio por cliente/rubro
- minimos de compra y condiciones
- historial y repeticion de pedidos
- entrega programada

## Fase 3 - Marketplace (posterior, no comprometida ahora)
**Incluye (a evaluar):**
- multi-store real
- onboarding de comercios
- comisiones/liquidaciones
- soporte y reclamos centralizados

---

## 6) Requisitos funcionales clave del MVP (Fase 1)
### Cliente final (B2C)
- ver catalogo y detalle de productos
- agregar/quitar items del carrito
- checkout con datos minimos
- elegir retiro o envio local
- recibir confirmacion con numero de pedido

### Admin del local
- login seguro
- bandeja de pedidos por estado
- cambio de estado con timestamp
- cancelar pedido con motivo
- alta/edicion/baja logica de productos
- configurar horario y pausa de pedidos

### Flujo de estados recomendado
`Nuevo -> En preparacion -> Listo -> Enviado/Retirado -> Cerrado`  
`Cancelado` como flujo alternativo.

---

## 7) Requisitos no funcionales
- mobile-first real
- performance web alta para catalogo
- validaciones server-side de pedidos y precios
- logs minimos de acciones criticas
- diseno de base con `store_id` desde inicio (preparado para escalar)

---

## 8) Arquitectura: opciones reales para decidir
## Opcion A - Astro + React Islands + API Node/Express (separada)
**Pros:**
- storefront muy rapido y SEO-friendly
- control fino del JS enviado al cliente
- backend reusable para futura app mobile

**Contras:**
- mas piezas operativas (frontend + backend separados)
- mayor friccion inicial en auth, CORS y despliegue

## Opcion B - Next.js Fullstack (frontend + api en una misma app)
**Pros:**
- menos complejidad operativa inicial
- menor overhead de integracion
- velocidad para MVP si equipo ya domina este flujo

**Contras:**
- puede sentirse mas pesado si no se optimiza bien
- menor separacion explicita de capas desde el dia 1

## Recomendacion de decision
Si la prioridad principal es **tiempo de salida + simplicidad operativa**, elegir Opcion B.  
Si la prioridad principal es **performance de storefront + reusable API separada**, elegir Opcion A.

---

## 9) Matriz de decision tecnica (1 a 5)
| Criterio | Peso | Opcion A Astro+API | Opcion B Next Fullstack |
|---|---:|---:|---:|
| Time-to-market MVP | 5 | 3 | 5 |
| Simplicidad operativa | 4 | 3 | 5 |
| Performance storefront | 4 | 5 | 4 |
| SEO inicial | 3 | 5 | 4 |
| Reuso API para mobile | 3 | 5 | 4 |
| Curva de trabajo actual | 4 | 4 | 5 |
| **Total ponderado** | - | **82** | **93** |

Interpretacion: con pesos orientados a entregar rapido y con bajo riesgo operativo, hoy gana Next Fullstack.  
Si sube el peso de performance pura y separacion de capas, Astro se vuelve mas competitivo.

---

## 10) Modelo de datos minimo sugerido
- `stores`
- `users` (roles: customer, store_admin, platform_admin futuro)
- `categories`
- `products`
- `product_variants` (opcional inicial)
- `orders`
- `order_items` (con snapshot de nombre/precio al momento de compra)
- `order_status_history`
- `store_settings` (horarios, pausa, delivery_rules)

---

## 11) API minima sugerida (independiente del frontend)
### Publicas
- `GET /catalog`
- `GET /products/:id`
- `POST /orders`

### Admin
- `POST /auth/admin/login`
- `GET /admin/orders`
- `PATCH /admin/orders/:id/status`
- `GET /admin/products`
- `POST /admin/products`
- `PATCH /admin/products/:id`
- `PATCH /admin/store/settings`

Regla no negociable: totales y validaciones de pedido se recalculan en backend.

---

## 12) Plan de ejecucion semanal (referencia)
### Semana 1-2 (Discovery)
- relevamiento
- reglas y alcance cerrado
- prototipo

### Semana 3-4
- base de datos
- autenticacion admin
- catalogo y productos

### Semana 5-6
- carrito/checkout
- creacion de pedidos
- panel de pedidos y estados

### Semana 7
- store settings (horarios, pausa, envio)
- QA funcional end-to-end

### Semana 8
- ajustes finales
- despliegue
- capacitacion y salida controlada

---

## 13) Estimacion economica por escenarios
## Escenario 1 (recomendado para arrancar)
- Discovery + Fase 1
- USD 6,000 - 10,000

## Escenario 2 (operacion consolidada)
- Discovery + Fase 1 + Fase 1.5
- USD 10,000 - 16,000

## Escenario 3 (incluye B2B inicial)
- Discovery + Fase 1 + Fase 1.5 + Fase 2
- USD 16,000 - 26,000

### Costos recurrentes estimados
- infraestructura: USD 30 - 120 / mes
- soporte/mantenimiento: USD 120 - 350 / mes

Nota: cotizar por fase con alcance cerrado evita sobrecostos por ambiguedad.

---

## 14) Modelo comercial recomendado
- modalidad por hitos
- anticipo 30%
- pagos por etapa: 30% inicio, 30% aprobacion funcional intermedia, 30% entrega, 10% salida productiva
- garantia: 30 dias de correccion de errores (sin nuevas features)
- cambios de alcance: gestionados como adicionales formales

---

## 15) Riesgos principales y mitigacion
| Riesgo | Impacto | Mitigacion |
|---|---|---|
| Querer incluir demasiado en Fase 1 | atrasos y sobrecostos | recorte estricto del MVP |
| Reglas de stock no definidas | errores operativos | taller de reglas en Discovery |
| Cambios constantes del cliente | deriva de alcance | backlog firmado por fase |
| Integraciones fiscales no planificadas | alta complejidad | dejar fuera de MVP y cotizar aparte |
| Exceso de complejidad tecnica inicial | baja velocidad | priorizar arquitectura mas simple para F1 |

---

## 16) Decisiones pendientes (checklist de estudio)
1. Arquitectura Fase 1: Opcion A (Astro+API) u Opcion B (Next fullstack).
2. Checkout: con cuenta obligatoria o invitado.
3. Metodo de pago inicial: solo efectivo/transferencia o incluir MercadoPago en F1.
4. Delivery: costo fijo, por zona o por radio.
5. Horarios: solo inmediato o tambien programado.
6. Mayorista en F1: solo consulta o mini flujo separado.
7. Nivel de reportes requerido para primer release.
8. Politica de soporte mensual deseada.

---

## 17) Criterios de Go/No-Go para lanzar Fase 1
- el cliente puede crear pedido completo (retiro y envio)
- admin puede procesar pedido de Nuevo a Cerrado
- horarios y pausa impactan en checkout correctamente
- totales se validan desde backend
- flujo probado en mobile y escritorio
- monitoreo basico activo

Si alguno falla, no se recomienda salida plena; hacer salida controlada.

---

## 18) Recomendacion final para tu caso
Para este cliente y este momento:
1. cerrar Discovery corto y pago
2. lanzar Fase 1 acotada sin sobreprometer
3. tomar decisiones con metricas reales de uso
4. recien ahi activar Fase 1.5 y Fase 2

Frase de posicionamiento:
"Primero resolvemos ventas online y operacion estable del local. Despues escalamos mayorista y automatizaciones con base real."

---

## 19) Proximo uso recomendado de este documento
- usarlo como base interna para alinear socios
- derivar una version comercial corta (1-2 paginas)
- derivar una version tecnica de ejecucion (tickets y backlog)
- usar la seccion 16 para reunion de decisiones antes de firmar alcance
