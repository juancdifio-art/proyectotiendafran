# Proyecto Tienda Online (Fase 1) - Decisiones, Alcance y Arquitectura (Brainstorming Consolidado)

> Documento consolidado en base a toda la conversacion: contexto del cliente, enfoque por fases, PRD Fase 1, decisiones de arquitectura (Astro/React islands + Node/Express/Prisma/Postgres), roadmap y criterios para escalar a futuro (distribuidora / marketplace tipo "PedidosYa Necochea").

---

## 0) Contexto del cliente (input de reunion)

- Cliente con **local a la calle** que vende:
  - **Comidas preparadas**
  - **Helados**
  - **Otra mercaderia**
- Ademas vende **alfajores al por mayor**, que tambien comercializa en el local.
  - Los alfajores los fabrica el padre del cliente, que tiene **distribuidora y fabrica de alfajores**.
  - Tambien fabrican **helados de agua**.
- En el local existe un software antiguo que el cliente casi no usa, posiblemente llamado **DataLife** (o similar).
- Objetivo del cliente:
  - Crear **tienda online** estilo "PedidosYa" pero para **Necochea**, con crecimiento progresivo.
  - **Fase 1:** solo su local en web app (y/o mobile app).
  - **Fase 2:** evaluar incorporar la distribuidora o hacerle un sistema propio (con interconexion opcional).
- Stack preferido por el equipo:
  - Se maneja fuerte **PERN / Next**, pero se evaluan alternativas por performance y DX.
  - Para mobile futuro: **React Native** (posible, no inmediato).

---

## 1) Enfoque producto: "marketplace despues, primero single-store"

### Decision central
**No construir marketplace desde el dia 1.**  
Arrancar con **single-store** (una tienda: el local) para vender rapido y validar operacion.

### Justificacion
Un marketplace tipo PedidosYa desde el comienzo explota complejidad en:
- roles y permisos multi-comercio
- onboarding de comercios
- pagos/retenciones/liquidaciones/comisiones
- logistica y soporte/reclamos
- administracion central y auditoria
- escalabilidad operativa antes de validar traccion

### Fases sugeridas
- **Fase 1 (MVP):** tienda online del local, flujo completo de pedido, admin simple.
- **Fase 1.5 (operacion):** pagos online (MercadoPago), comandas/impresion, reportes.
- **Fase 2:** modulo distribuidora / B2B (mayorista real) o backoffice mas avanzado.
- **Fase 3:** "PedidosYa Necochea" (multi-comercio + comisiones + onboarding).

---

## 2) Alcance MVP Fase 1 (lo minimo que realmente vende)

### Cliente (frontend)
- Catalogo por categorias:
  - Comidas preparadas / Helados / Mercaderia / Alfajores
- Producto con variantes simples (si aplica):
  - sabores / tamanos / packs (ej. docena / caja mayorista)
- Carrito + checkout
- Entrega:
  - **Retiro en local**
  - **Envio local en Necochea** (con costo simple)
- Pago:
  - Arranque recomendado: **efectivo / transferencia**
  - MercadoPago: ideal en Fase 1.5 (cuando el flujo este aceitado)
- Confirmacion:
  - Confirmacion en pantalla con ID de pedido
  - (Opcional) link a WhatsApp para consultas

### Operacion / Admin
- Panel de pedidos:
  - estados: `Nuevo -> En preparacion -> Listo -> Enviado/Retirado -> Cerrado/Cancelado`
- Gestion de productos:
  - CRUD basico
  - habilitar/deshabilitar productos
- Horarios del local + "pausar pedidos"
- Zona/costo de entrega:
  - costo fijo o por zona simple

### Fuera de alcance Fase 1 (explicito)
- Stock perfecto en tiempo real
- Promos complejas / cupones / puntos
- Tracking repartidores
- Multi-sucursal y multi-comercio
- Integracion con DataLife desde el dia 1 (salvo que sea imprescindible y tenga API usable)

---

## 3) Escalabilidad planificada sin sobredisenar

### Decision: modelar como si fuera multi-store desde DB, aunque haya 1 solo store
Desde el dia 1 se crean conceptos:
- `stores` (aunque exista solo 1)
- `products.store_id`
- `orders.store_id`
- Roles: `customer`, `store_admin`, (futuro) `platform_admin`

### Beneficios
- Permite sumar otra tienda mas adelante sin reescritura grande
- Prepara el salto a marketplace (Fase 3)
- Mantiene un camino claro para integrar distribuidora y B2B

---

## 4) Mayorista (alfajores B2B) vs Minorista (B2C): separacion conceptual

### Hallazgo importante
El mayorista trae reglas diferentes:
- listas de precio por volumen
- minimos de compra
- clientes registrados/aprobacion
- envio fuera de Necochea / logistica distinta
- condiciones de pago/facturacion

### Decision recomendada
- **Fase 1:** mayorista como "catalogo + consulta" o pedido simple separado, sin reglas complejas.
- **Fase 2:** modulo B2B real (precios por cliente, minimos, estados, logistica, etc.)

---

## 5) Decisiones criticas a cerrar temprano (preguntas que definen el alcance real)

Estas preguntas son "gates" del alcance:

1. Entrega: ?solo Necochea? ?radio fijo? ?costo por zona?
2. Horarios: ?permiten programar pedidos o solo inmediato?
3. Pagos: ?efectivo/transferencia al inicio? ?MercadoPago obligatorio?
4. Pedido minimo: ?minimo para envio?
5. Helados: ?restricciones/logistica (tiempos, franjas)?
6. Comidas: ?menu cambia por dia? (muy comun)
7. Mayorista: ?requiere aprobacion? ?clientes recurrentes?
8. Datos del cliente: ?direccion + referencias + telefono minimo?
9. Operacion: ?comanda/impresion o solo pantalla?
10. DataLife: ?que hace exactamente y por que no lo usan?

> Nota: DataLife se trata como "legacy" y no se integra en Fase 1 salvo necesidad.

---

## 6) PRD - Fase 1 (MVP) (resumen completo)

### 6.1 Resumen
- **Objetivo:** lanzar tienda online mobile-first para el local, recibir/gestionar pedidos con base escalable.
- **Alcance:** 1 store, web app, panel admin simple, retiro/envio local.
- **No objetivo:** marketplace, tracking, liquidaciones, promos avanzadas, integracion legacy.

### 6.2 Stakeholders
- Dueno/operacion (admin)
- Cliente final (customer)
- Equipo dev

### 6.3 Problema
Falta canal digital ordenado: se busca vender + ordenar pedidos + reducir errores + habilitar iteracion rapida.

### 6.4 KPIs sugeridos
- conversion visita->pedido
- tiempo confirmacion/preparacion
- % cancelaciones
- pedidos/dia + ticket promedio
- % retiro vs envio

### 6.5 Requisitos funcionales (Cliente)
- Catalogo (categorias, detalle)
- Variantes simples + observaciones
- Carrito
- Checkout:
  - datos minimos (nombre, telefono)
  - entrega (retiro/envio), direccion si envio
  - franja horaria opcional
- Confirmacion con ID y estado `Nuevo`

### 6.6 Requisitos funcionales (Admin)
- Login admin
- Bandeja de pedidos por estado
- Cambio de estados + motivo cancelacion
- CRUD productos (+ categorias opcional)
- Config store:
  - horarios
  - pausar pedidos
  - configuracion delivery y costo

### 6.7 No funcionales
- performance mobile
- seguridad (server-side validation de totals, rate limit basico)
- auditabilidad minima (timestamps de cambios)
- extensibilidad con `store_id`

### 6.8 Reglas de negocio
- si el local esta cerrado/pausado, no se confirma pedido (salvo programado futuro)
- costo de envio por regla simple
- el backend recalcula precios/totales al crear pedido (anti-tampering)

### 6.9 Modelo de datos (alto nivel)
- Store, Product, Category, Order, OrderItem, AdminUser
- snapshots de items en OrderItem para preservar precio/nombre al momento del pedido

### 6.10 Criterios de aceptacion minimos
1. Cliente completa pedido retiro/envio y obtiene ID
2. Admin ve pedido en `Nuevo` y lo lleva a `Cerrado`/`Cancelado`
3. Admin puede pausar pedidos y editar productos
4. Si esta cerrado, checkout bloquea con mensaje claro

---

## 7) Diagrama simple - Flujo de pedido (Cliente -> Admin -> Cierre)

```mermaid
flowchart TD
  A[Cliente entra a la tienda] --> B[Explora catalogo / categorias]
  B --> C[Agrega productos al carrito]
  C --> D[Checkout: datos + entrega (retiro/envio)]
  D --> E{Local abierto y acepta pedidos?}
  E -- No --> E1[Mostrar "Cerrado / Pausado"\nNo permite confirmar] --> B
  E -- Si --> F[Crear pedido (status: Nuevo)]
  F --> G[Confirmacion al cliente\nID + resumen]

  F --> H[Admin: bandeja de pedidos\n(Nuevo)]
  H --> I{Admin acepta?}
  I -- Cancelar --> J[Status: Cancelado\nMotivo] --> K[Notificar cliente (opcional)]
  I -- Aceptar --> L[Status: En preparacion]
  L --> M[Status: Listo]
  M --> N{Entrega}
  N -- Retiro --> O[Cliente retira] --> P[Status: Cerrado]
  N -- Envio --> Q[Se envia pedido] --> R[Status: Enviado/Entregado] --> P[Status: Cerrado]
```

---

## 8) Decision de stack: objetivo "ultra rapido + SEO" (y por que)

### Observacion del usuario
- Next "se siente lento" (DX/performance percibida), mientras React + Vite volaba.
- Se asume que Astro puede dar una experiencia similar o mejor para storefront, especialmente por:
  - HTML-first / JS minimo
  - SSG por defecto
  - Islands para interactividad puntual

### Decision preferida
- Astro SSG + React islands + backend separado Node/Express/Prisma + Postgres.

### ?Next queda descartado?
- Next no es malo y puede servir, pero no es necesario si el objetivo principal es:
  - storefront ultra liviano/SEO
  - separar backend como API limpia (reutilizable para mobile y futuros proyectos)
- Next suele ser mas conveniente si se quiere:
  - monorepo fullstack (SSR/ISR + API + admin todo junto)
  - menos piezas de infraestructura
- En este caso se prioriza performance/SEO + preferencia personal por MVC en Express.

---

## 9) Importante: "ISG puro" no aplica a un sistema de pedidos

### Conclusion
No conviene "ISG puro" porque un sistema de pedidos es inherentemente dinamico:
- creacion de pedido (POST)
- validacion server-side de precios/totales
- horarios/pausar pedidos
- calculo de envio
- panel admin

### Patron correcto con Astro
- Astro hibrido (SSG para catalogo + APIs dinamicas para pedidos/admin)
- SSG/SEO:
  - home
  - categorias
  - producto
- Dinamico por API:
  - `POST /orders`
  - `GET /admin/orders`
  - `PATCH /admin/orders/:id/status`
  - auth admin

---

## 10) React en Astro: "Islands" (adopcion gradual)

### Decision
Usar React dentro de Astro solo donde haya interactividad real:
- carrito
- checkout
- admin (si se incluye dentro del mismo proyecto)

### Beneficio
- El resto del sitio queda estatico y rapido (SEO/Lighthouse).
- React no "contamina" todo el render como SPA completa.

### Aprendizaje
Astro se puede adoptar de forma incremental:
- paginas estaticas + layouts
- data fetch server-side para generar HTML
- agregar 1 island (carrito)
- expandir islands (checkout / admin)

---

## 11) Backend: Node/Express/Prisma (MVC) - decision por experiencia y gusto

### Decision
Backend separado: Node + Express + Prisma + Postgres, estilo MVC.

### Justificacion
- el equipo ya domina este enfoque
- permite velocidad de ejecucion en MVP
- deja API reutilizable para:
  - app mobile futura
  - paneles internos
  - marketplace futuro (Fase 3)
  - modulo B2B (Fase 2)

### Nota
Se menciono que Express no es el unico: Fastify/Hono pueden ser alternativas,
pero para MVP gana:
- estabilidad
- familiaridad
- velocidad de entrega

---

## 12) Principio de seguridad y consistencia: "backend = source of truth"

### Decision no negociable
Aunque el catalogo sea SSG y el cliente vea precios, al crear pedido el backend:
- vuelve a buscar productos en DB
- recalcula totales
- aplica reglas (envio, minimos, horarios)
- guarda snapshots en OrderItem

Esto evita:
- manipulacion del carrito/precios del lado cliente
- inconsistencias por rebuilds/caches

---

## 13) Roadmap consolidado (sin humo)

### Fase 1 (vende)
- catalogo SSG + React islands (carrito/checkout)
- pedidos retiro/envio
- admin pedidos + estados
- CRUD productos
- store settings (horarios/pausa/costo envio)
- confirmacion con ID

### Fase 1.5 (operacion)
- MercadoPago
- comanda/impresion (si lo piden)
- reportes basicos (ventas por dia/producto)

### Fase 2 (distribuidora / B2B)
- clientes B2B
- listas de precio + minimos
- estado de pedidos B2B
- logistica y facturacion basica
- integracion con sistemas (si conviene) - opcional

### Fase 3 (marketplace Necochea)
- onboarding de comercios
- comisiones y liquidaciones
- soporte/reclamos
- administracion central
- multi-store real

---

## 14) Deploy/Infra (lineas generales)

### Frontend (Astro SSG)
- deploy ideal en CDN:
  - Vercel / Cloudflare Pages / Netlify (segun preferencia)
- paginas estaticas = baratas y rapidas

### Backend (Express API)
- deploy como servicio:
  - Cloud Run / Render / Railway / Fly (segun costos y experiencia)

### Postgres
- Neon / Supabase / Postgres administrado

### Imagenes
- Cloudinary o Supabase Storage
- en DB solo URLs

---

## 15) Posicionamiento comercial (para cerrar sin vender humo)

### Decision de pitch
Venderlo como:
- "Sistema de pedidos digital del local" (Fase 1)
- con base tecnica lista para escalar a:
  - B2B distribuidora
  - marketplace multi-comercio (futuro)

### Modelo de cobro sugerido
- implementacion Fase 1 (proyecto)
- mantenimiento mensual (hosting/soporte/mejoras)
- Fase 2/3 como proyectos separados (no prometer todo desde el inicio)

---

## 16) Resultado: Decision final de stack (consolidada)

### Frontend
- Astro (SSG / SEO-first)
- Tailwind
- React (islands) para interactividad puntual

### Backend
- Node.js + Express
- Prisma (ORM)
- Arquitectura MVC (Controllers/Services/Repositories)

### DB
- PostgreSQL

### Principios clave
- SSG para SEO y velocidad
- APIs dinamicas para pedidos/admin
- backend valida precios/reglas al crear pedido
- modelo DB preparado para multi-store desde el dia 1 (`store_id`)

---

## 17) Notas de continuidad

Este documento consolida decisiones para el proyecto actual del local en Necochea.

Se dejo explicito que existe un proyecto futuro "mucho mas grande" de tienda virtual donde Astro tambien seria util, por lo que esta Fase 1 sirve ademas como:
- validacion de producto
- practica de Astro + islands
- base reutilizable del API y modelos
