Estoy pensando como encarar el proyecto de un potencial cliente, tuvimos una reunion entre mi socio, mi cliente y yo, y ahora paso a darte la informacion. El cliente tiene local a la calle de Comidas preparadas, Helados, y otra mercaderia. A su vez vende al por mayor Alfajores (que tambien vende en el local), los fabrica su padre que tiene una distribuidora y fabrica de alfajores, ademas fabrican helados de agua. En el local posee un software que lo tiene hace muchos años, y si no me equivoco se llama DataLife o algo asi, pero no lo usa demasiado. El cliente quiere crear una tienda online, similar a 'Pedidos Ya' pero para Necochea, y puede ir escalando progresivamente. En un principio tendria solo su local en la web app y/o mobile app. Luego en fase 2 se analizaria si incorporar la distribuidora o hacerle un sistema propio, pero que puede tener una interconexion o no. El stack que mas manejo es PERN Next y creo que es el mas adecuado, aunque para mobile quizas utilice ReactNative. Esto es un brainstorming.

Perfecto. Si lo encarás como “PedidosYa local” pero con **evolución controlada**, lo más importante es **no sobrediseñar** la Fase 1 y, a la vez, dejar “ganchos” claros para escalar a marketplace y/o integrar la distribuidora.

Abajo te dejo un enfoque bien práctico, con **fases**, **alcance MVP**, **arquitectura PERN/Next**, y **decisiones clave**.

---

## 1) Enfoque producto: marketplace *después*, primero “single-store”

**Fase 1 (MVP):** una tienda online del local (web app mobile-first).
Objetivo: vender *hoy*, validar flujo de pedidos, operación y logística.

**Fase 2:** sumar distribuidora (B2B) o backoffice avanzado (stock, precios por canal, etc.).
**Fase 3:** recién ahí pensar “PedidosYa Necochea” (multi-comercio, comisiones, onboarding, etc.).

> Si intentás marketplace desde el día 1, te explota en: roles, pagos, logística, soporte, onboarding, reclamos, etc.

---

## 2) MVP Fase 1: alcance mínimo que realmente vende

### Cliente (frontend)

* Catálogo por categorías: **Comidas preparadas / Helados / Mercadería / Alfajores**
* Producto con variantes simples:

  * sabores / tamaños / packs (ej: docena alfajores / caja mayorista)
* Carrito + checkout
* Opciones de entrega:

  * **Retiro en local**
  * **Envío local** (Necochea): con franjas horarias o “lo antes posible”
* Pago:

  * **Cash/transferencia** al inicio (cero fricción operativa)
  * Luego MercadoPago (cuando el flujo esté aceitado)
* Confirmación:

  * WhatsApp deep link (“Enviar pedido”) o confirmación dentro del sistema + notificación

### Operación (admin)

* Panel simple de pedidos:

  * estados: `Nuevo → En preparación → Listo → Enviado/Retirado → Cerrado/Cancelado`
* Gestión de productos:

  * CRUD + habilitar/deshabilitar
  * precio, descripción, foto, categoría
* Horarios del local + “pausar pedidos”
* Zona de entrega (por barrios / radio aproximado) + costo de envío fijo o por zona

**Lo que NO metería en MVP** (salvo que sea imprescindible):

* Stock en tiempo real “perfecto”
* Promociones complejas, cupones, puntos
* Repartidores con tracking
* Multi-sucursal, multi-comercio
* Integración con “DataLife” desde el día 1 (salvo que ya tenga API y realmente la use)

---

## 3) Diseño pensando en escalabilidad: “de single-store a multi-store”

Aunque arranques con un comercio, definí desde el principio estos conceptos en DB:

* `stores` (aunque haya 1 sola)
* `products.store_id`
* `orders.store_id`
* `users` con roles: `customer`, `store_admin`, (futuro) `platform_admin`

Eso te habilita a futuro:

* sumar otra tienda sin reescribir medio sistema
* convertirlo en marketplace (Fase 3) con menos dolor

---

## 4) Arquitectura recomendada con tu stack (PERN + Next)

Para Fase 1 yo haría **Next.js fullstack** (App Router) y evitaría Express separado, salvo que ya tengas un backend estándar tuyo.

**Propuesta:**

* **Next.js (App Router)**

  * UI + API Routes (REST)
* **PostgreSQL** (Neon/Supabase)
* **Prisma** (si ya venís migrando a Prisma, te conviene)
* **Auth**:

  * clientes: opcional login (podés permitir checkout como invitado con teléfono)
  * admin: login obligatorio + 2FA opcional (más adelante)
* **Uploads**: Supabase Storage / Cloudinary (cualquiera; guardás URL en DB)

**Notificaciones:**

* MVP: WhatsApp link
* Fase 1.5: email / push / SMS (según costo/valor)

---

## 5) Dos líneas de negocio distintas: B2C vs B2B (alfajores mayorista)

Acá está la trampa típica: **mayorista** trae reglas distintas.

* precios por volumen
* mínimos de compra
* facturación/condiciones
* envío fuera de Necochea
* clientes “registrados”

**Recomendación:**

* En Fase 1: mayorista **solo como “catálogo + consulta”** o “pedido mayorista” separado con reglas simples.
* En Fase 2: módulo B2B real (listas de precio, mínimos, estados, etc.)

---

## 6) Decisiones críticas que tenés que cerrar temprano (para no rehacer)

Estas 10 preguntas te definen el alcance real:

1. **Entrega:** ¿solo Necochea? ¿hay radio fijo? ¿costo por zona?
2. **Horarios:** ¿permiten programar pedidos?
3. **Pagos:** ¿arrancan con efectivo/transferencia? ¿quieren MercadoPago sí o sí?
4. **Pedido mínimo:** ¿hay mínimo para envío?
5. **Helados:** ¿requiere logística especial? (tiempo máximo, franja horaria)
6. **Comidas:** ¿menú cambia por día? (muy común)
7. **Mayorista:** ¿es “pedido recurrente” a negocios? ¿requiere aprobación?
8. **Datos del cliente:** ¿piden dirección exacta + referencias + teléfono?
9. **Impresión/Comanda:** ¿quieren ticket en cocina o con ver en pantalla alcanza?
10. **El software viejo (DataLife):** ¿qué hace exactamente y por qué no lo usan? (si no es core, no tocarlo)

---

## 7) Roadmap sugerido (sin humo, bien incremental)

**Fase 1 (vende):**

* catálogo + carrito + pedido + panel de pedidos + retiro/envío + WhatsApp/confirmación

**Fase 1.5 (mejora operación):**

* MercadoPago
* impresión/comanda
* reportes simples (ventas por día/producto)

**Fase 2 (distribuidora / B2B):**

* clientes B2B, listas de precio, mínimos, estados, envíos, facturación básica

**Fase 3 (marketplace Necochea):**

* onboarding comercios
* comisiones, liquidaciones
* soporte/reclamos
* multi-tienda, multi-categoría, administración central

---

## 8) Consejo comercial (para cerrar sin regalarte)

Vendelo como:

* **“Sistema de pedidos digital del local”** (Fase 1)
* con **“base lista para crecer a plataforma multi-comercio”** (sin prometer el mundo hoy)

Y cobrás por:

* implementación Fase 1
* mantenimiento mensual (hosting + soporte + mejoras)
* Fase 2/3 como “proyectos” separados

---

Si querés, en el próximo mensaje te armo:

* un **PRD** (documento de requisitos) Fase 1 en 1–2 páginas
* un **esquema de DB (Prisma)** mínimo
* y un **diagrama simple de flujo de pedido** (cliente → admin → cierre).


armame un PRD (documento de requisitos) Fase 1 en 1–2 páginas y un diagrama simple de flujo de pedido (cliente → admin → cierre).

## PRD — Fase 1 (MVP) Tienda Online “Single-Store” (Necochea)

### 1. Resumen

**Objetivo:** lanzar una tienda online mobile-first para el **local** (comidas preparadas, helados, mercadería, alfajores) que permita **recibir y gestionar pedidos** con mínima fricción operativa y base lista para escalar (futuro multi-store / B2B).

**Alcance Fase 1:** 1 comercio (1 “store”), web app (PWA opcional), panel admin simple, pedidos por retiro o envío local.

**No objetivo (explicitamente fuera de alcance F1):** marketplace multi-comercio, tracking repartidores, liquidaciones/comisiones, promociones avanzadas, stock perfecto en tiempo real, integración con “DataLife”.

---

### 2. Stakeholders

* **Dueño/Operación del local (Admin Store):** necesita recibir, preparar y cerrar pedidos.
* **Clientes finales (Customer):** quieren comprar rápido desde el celular.
* **Equipo dev (Nosotros):** entrega MVP estable + extensible.

---

### 3. Problema a resolver

Hoy el negocio no tiene un canal digital propio (o no está optimizado). El MVP debe:

* aumentar ventas por canal online
* ordenar la gestión de pedidos (menos WhatsApp caótico)
* reducir errores de preparación/entrega
* permitir iteración rápida (precios, menú, horarios)

---

### 4. Objetivos y métricas (KPIs)

**Objetivos de negocio:**

* Lanzar en producción con flujo completo de pedido.
* Lograr adopción local con mínima fricción.

**KPIs sugeridos (F1):**

* Tasa de conversión: visitas → pedido
* Tiempo promedio de confirmación/preparación
* % pedidos cancelados
* Pedidos por día y ticket promedio
* % retiro vs envío

---

### 5. Supuestos y restricciones

* Zona primaria: **Necochea**.
* F1 admite **checkout sin cuenta** (recomendado) para reducir fricción.
* Pagos F1: **efectivo/transferencia** (MercadoPago se evalúa F1.5).
* Entrega: **retiro** y/o **envío local** (costo fijo o por zona simple).

---

### 6. Requisitos funcionales

#### 6.1. Cliente (Web app)

**RF-C1 Catálogo**

* Ver productos por categorías (Comidas / Helados / Mercadería / Alfajores).
* Ver detalle: nombre, descripción, precio, imagen, disponibilidad (habilitado/pausado).

**RF-C2 Variantes y extras (simple)**

* Variantes opcionales (p.ej. tamaño, sabor, pack) con ajuste de precio.
* Observaciones del cliente (texto libre) con límite (ej: 250 chars).

**RF-C3 Carrito**

* Agregar/quitar items, modificar cantidad.
* Ver subtotal + costo de envío (si aplica).

**RF-C4 Checkout**

* Datos mínimos: nombre, teléfono, método de entrega.
* Si **envío**: dirección, referencias, barrio/zona (si se usa).
* Selección: “Lo antes posible” o franja horaria (si se habilita en F1).
* Confirmación final del pedido con resumen.

**RF-C5 Confirmación y seguimiento**

* Mostrar pantalla de “Pedido recibido” con ID y estado inicial “Nuevo”.
* (Opcional MVP) link a WhatsApp para consultas.

#### 6.2. Admin (Panel del local)

**RF-A1 Login Admin**

* Acceso restringido a usuarios admin del local.

**RF-A2 Bandeja de pedidos**

* Lista de pedidos por estado: `Nuevo`, `En preparación`, `Listo`, `Enviado/Retirado`, `Cerrado`, `Cancelado`.
* Detalle completo del pedido (items, observaciones, datos cliente, entrega).

**RF-A3 Gestión de estados**

* Cambiar estado con un click (y timestamp).
* Motivo de cancelación (texto corto).

**RF-A4 Gestión de productos**

* CRUD productos: nombre, descripción, precio, categoría, imagen, habilitado/pausado.
* CRUD categorías (opcional si se predefinen inicialmente).
* CRUD variantes simples (opcional F1; si complica, se posterga a F1.5).

**RF-A5 Configuración del local (Store Settings)**

* Horarios (open/close por día).
* Pausar pedidos (modo “cerrado” manual).
* Configurar opciones de entrega: retiro / envío.
* Configurar costo de envío simple:

  * fijo
  * o por zona (lista simple)

---

### 7. Requisitos no funcionales

* **RNF-1 Performance:** catálogo debe cargar rápido en móvil (LCP razonable).
* **RNF-2 Disponibilidad:** tolerar picos chicos (fines de semana).
* **RNF-3 Seguridad:** panel admin protegido; validación server-side de precios/items; rate limiting básico.
* **RNF-4 Auditabilidad:** logs mínimos de cambios de estado de pedidos.
* **RNF-5 Extensibilidad:** modelo DB con `store_id` aunque haya un solo store.

---

### 8. Reglas de negocio (F1)

* No se permite pedido si el local está “cerrado” (por horario o manual), salvo que se habilite “programado”.
* Costo de envío se calcula por regla simple (fijo o por zona).
* Pedido mínimo para envío (opcional; si existe, bloquear checkout envío si no se cumple).
* Precios se toman del servidor al crear pedido (evitar manipulación del cliente).

---

### 9. Modelo de datos (alto nivel)

* **Store**: configuración, horarios, delivery rules.
* **Product**: store_id, category_id, price, enabled.
* **Category**: store_id, name.
* **Order**: store_id, status, totals, delivery_type, delivery_address, customer_contact.
* **OrderItem**: order_id, product_snapshot (nombre/precio al momento), qty, notes.
* **AdminUser**: store_id, role.

---

### 10. Experiencia UX (mínima)

* Mobile-first, 3 pasos: catálogo → carrito → checkout.
* “Reordenar” (repetir pedido) se deja para F1.5.
* Accesibilidad básica: contraste, tamaños táctiles, estados claros.

---

### 11. Criterios de aceptación (mínimos)

1. Un cliente puede completar un pedido con retiro o envío y recibe confirmación con ID.
2. El admin ve el pedido en “Nuevo” y puede pasarlo por estados hasta “Cerrado” o “Cancelado”.
3. El admin puede pausar pedidos y editar productos (precio/habilitado).
4. Si el local está cerrado, el checkout no permite confirmar pedido (mensaje claro).

---

## Diagrama simple — Flujo de pedido (Cliente → Admin → Cierre)

```mermaid
flowchart TD
  A[Cliente entra a la tienda] --> B[Explora catálogo / categorías]
  B --> C[Agrega productos al carrito]
  C --> D[Checkout: datos + entrega (retiro/envío)]
  D --> E{Local abierto y acepta pedidos?}
  E -- No --> E1[Mostrar "Cerrado / Pausado"\nNo permite confirmar] --> B
  E -- Sí --> F[Crear pedido (status: Nuevo)]
  F --> G[Confirmación al cliente\nID + resumen]

  F --> H[Admin: bandeja de pedidos\n(Nuevo)]
  H --> I{Admin acepta?}
  I -- Cancelar --> J[Status: Cancelado\nMotivo] --> K[Notificar cliente (opcional)]
  I -- Aceptar --> L[Status: En preparación]
  L --> M[Status: Listo]
  M --> N{Entrega}
  N -- Retiro --> O[Cliente retira] --> P[Status: Cerrado]
  N -- Envío --> Q[Se envía pedido] --> R[Status: Enviado/Entregado] --> P[Status: Cerrado]
```

Si querés, en el próximo paso te lo convierto a:

* checklist de implementación por módulos (frontend/admin/api/db)
* y una versión “para cliente” (más comercial, menos técnica) en 1 página.
