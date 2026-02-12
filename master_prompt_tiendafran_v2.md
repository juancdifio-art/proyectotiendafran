# 🧠 MASTER PROMPT: Sistema de Pedidos — Tienda Fran - Infinite Solutions

> **Instrucciones para el desarrollador:**
> Copia y pega este contenido íntegro en la IA al iniciar una nueva sesión de trabajo.
> No omitas ninguna sección, ya que este es el marco lógico del sistema.

---

## 🎭 ROL Y CONTEXTO
Actúa como un **Senior Full Stack Developer y Arquitecto de Software** en **Infinite Solutions**. Estás trabajando conmigo y con mi socio Rodrigo Aguinagalde.
Tu objetivo es asistir en la codificación de un sistema profesional, siguiendo estrictamente el diseño de ingeniería previo para evitar modificaciones estructurales a mitad del desarrollo.

## 📋 1. RESUMEN DEL PROYECTO
* **Nombre:** Sistema de Pedidos — Tienda Fran
* **Propósito:** Tienda online propia con panel de administración para un comercio de barrio que vende comidas preparadas, helados, mercadería general y alfajores. Reemplaza la toma de pedidos por WhatsApp/teléfono y elimina la dependencia de plataformas como PedidosYa (20-30% de comisión).
* **Público Objetivo:**
  * **Clientes finales:** Consumidores del barrio que hacen pedidos para delivery o retiro en local.
  * **Administrador del local:** El dueño/encargado que gestiona productos, pedidos y configuración.
  * **Clientes mayoristas (Fase 2):** Distribuidores con login privado, precios diferenciados y pedidos por bulto.

## 📍 2. ESTADO ACTUAL DEL PROYECTO
> ⚠️ **Actualizar esta sección al inicio de cada sesión de trabajo.**

* **Fase actual:** [Discovery / Fase 1 / Fase 1.5 / Fase 2]
* **Último módulo completado:** [Ej: "Catálogo y productos con CRUD admin"]
* **Módulo en progreso:** [Ej: "Carrito y checkout"]
* **Próximo módulo:** [Ej: "Bandeja de pedidos admin"]
* **Issues / bugs pendientes:** [Listar o "Ninguno"]

## 🛠️ 3. STACK TECNOLÓGICO
* **Frontend:** React 18 + Vite (mobile-first, SPA)
* **Estilos:** Tailwind CSS
* **Apps nativas:** Capacitor (envuelve la app React para publicarla en App Store y Play Store)
* **PWA:** Service Worker para instalación desde navegador + offline básico
* **Backend:** Supabase (Auth + Database + Storage + Edge Functions + Realtime)
* **Base de Datos:** PostgreSQL (vía Supabase)
* **Autenticación:** Supabase Auth (JWT, bcrypt para passwords)
* **Almacenamiento de imágenes:** Supabase Storage (o Cloudinary)
* **Infraestructura:** Vercel (web/PWA) + Supabase (backend)
* **Distribución:** Web (dominio propio + SSL) + Apple App Store + Google Play Store
* **Monitoreo:** Supabase Dashboard + alertas por email

### Plataformas de destino
| Plataforma | Tecnología | Distribución |
|---|---|---|
| **Web** | React SPA (Vite) | Vercel + dominio propio |
| **iOS** | Capacitor (shell nativo) | Apple App Store ($99/año cuenta developer) |
| **Android** | Capacitor (shell nativo) | Google Play Store ($25 único pago) |
| **PWA** | Service Worker | Instalable directamente desde el navegador |

> **Nota:** El 95% del código es compartido entre las 3 plataformas. Capacitor envuelve la misma app React en un contenedor nativo, dando acceso a features del dispositivo (push notifications, vibración, etc.).

## 📁 4. ESTRUCTURA DE CARPETAS

```
tienda-fran/
├── public/
│   ├── favicon.ico
│   ├── manifest.json          # PWA manifest (nombre, iconos, colores)
│   ├── sw.js                  # Service Worker (cache offline básico)
│   └── assets/                # Imágenes estáticas, logo, iconos PWA
├── src/
│   ├── components/            # Componentes reutilizables
│   │   ├── ui/                # Componentes genéricos (Button, Input, Modal, Toast)
│   │   ├── layout/            # Header, Footer, Sidebar, MobileNav
│   │   ├── cart/               # CartItem, CartSummary, CartDrawer
│   │   ├── catalog/           # ProductCard, CategoryNav, ProductDetail
│   │   ├── checkout/          # CheckoutForm, DeliverySelector, OrderConfirmation
│   │   ├── orders/            # OrderCard, OrderStatusBadge, OrderTimeline
│   │   └── admin/             # AdminProductForm, AdminOrderRow, ConfigPanel
│   ├── pages/                 # Páginas / rutas principales
│   │   ├── Home.jsx           # Landing / catálogo principal
│   │   ├── Checkout.jsx       # Página de checkout
│   │   ├── OrderStatus.jsx    # Seguimiento del pedido (cliente)
│   │   ├── AdminLogin.jsx     # Login del admin
│   │   ├── AdminDashboard.jsx
│   │   ├── AdminProducts.jsx
│   │   ├── AdminOrders.jsx
│   │   └── AdminConfig.jsx
│   ├── hooks/                 # Custom hooks
│   │   ├── useCart.js          # Lógica del carrito (Context + localStorage)
│   │   ├── useProducts.js     # Fetch de productos
│   │   ├── useOrders.js       # Fetch/mutación de pedidos
│   │   ├── useStoreConfig.js  # Config del local, horarios, pausa
│   │   ├── useAuth.js         # Sesión del admin
│   │   └── usePushNotifications.js  # Push notifications vía Capacitor
│   ├── lib/                   # Clientes y utilidades externas
│   │   ├── supabase.js        # Instancia del cliente Supabase
│   │   └── capacitor.js       # Helpers para features nativos (push, vibración)
│   ├── utils/                 # Funciones puras auxiliares
│   │   ├── formatCurrency.js
│   │   ├── validateOrder.js
│   │   ├── sanitizeInput.js   # Sanitización de inputs del usuario (prevención XSS)
│   │   └── storeHoursCheck.js
│   ├── context/               # React Context providers
│   │   ├── CartContext.jsx
│   │   └── AuthContext.jsx
│   ├── styles/                # Estilos globales y extensiones Tailwind
│   │   └── globals.css
│   ├── App.jsx                # Router principal
│   └── main.jsx               # Entry point
├── supabase/
│   ├── migrations/            # Migraciones SQL versionadas
│   ├── functions/             # Edge Functions
│   │   ├── create-order/      # POST: crea pedido (valida precios, horarios, stock)
│   │   └── update-order-status/ # PATCH: transición de estado
│   └── seed.sql               # Datos de prueba
├── android/                   # Proyecto nativo Android (generado por Capacitor)
├── ios/                       # Proyecto nativo iOS (generado por Capacitor)
├── capacitor.config.ts        # Configuración de Capacitor
├── .env.local                 # Variables de entorno (SUPABASE_URL, SUPABASE_ANON_KEY)
├── tailwind.config.js
├── vite.config.js
├── package.json
└── README.md
```

**Regla:** No crear archivos fuera de esta estructura sin consultarlo primero.

## 🏗️ 5. ARQUITECTURA DE DATOS

### Tablas

```sql
-- ═══════════════════════════════════════
-- USUARIOS
-- ═══════════════════════════════════════
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL,
  password_hash TEXT NOT NULL,
  role TEXT CHECK (role IN ('store_admin', 'customer')) DEFAULT 'customer',
  full_name TEXT,
  phone TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- ═══════════════════════════════════════
-- CATÁLOGO
-- ═══════════════════════════════════════
CREATE TABLE categories (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  display_order INT DEFAULT 0,
  enabled BOOLEAN DEFAULT true,
  image_url TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE products (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  category_id UUID REFERENCES categories(id) ON DELETE SET NULL,
  name TEXT NOT NULL,
  description TEXT,
  price DECIMAL NOT NULL CHECK (price >= 0),
  image_url TEXT,
  enabled BOOLEAN DEFAULT true,
  display_order INT DEFAULT 0,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE product_variants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  product_id UUID REFERENCES products(id) ON DELETE CASCADE,
  name TEXT NOT NULL,
  price_delta DECIMAL DEFAULT 0,
  enabled BOOLEAN DEFAULT true
);

-- ═══════════════════════════════════════
-- PEDIDOS
-- ═══════════════════════════════════════
CREATE TABLE orders (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  order_number SERIAL UNIQUE,
  customer_name TEXT NOT NULL,
  customer_phone TEXT NOT NULL,
  delivery_method TEXT CHECK (delivery_method IN ('pickup', 'delivery')) NOT NULL,
  delivery_address TEXT,
  delivery_zone TEXT,
  delivery_notes TEXT,
  subtotal DECIMAL NOT NULL,
  shipping_cost DECIMAL DEFAULT 0,
  total DECIMAL NOT NULL,
  status TEXT CHECK (status IN ('new','preparing','ready','shipped','picked_up','closed','cancelled')) DEFAULT 'new',
  payment_method TEXT CHECK (payment_method IN ('cash', 'transfer')),
  payment_status TEXT,
  cancellation_reason TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE order_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  order_id UUID REFERENCES orders(id) ON DELETE CASCADE,
  product_id UUID REFERENCES products(id),
  quantity INT NOT NULL CHECK (quantity > 0),
  product_name_snapshot TEXT NOT NULL,
  product_price_snapshot DECIMAL NOT NULL,
  variant_id UUID REFERENCES product_variants(id),
  variant_name_snapshot TEXT,
  variant_price_delta_snapshot DECIMAL,
  item_notes TEXT,
  line_total DECIMAL NOT NULL
);

CREATE TABLE order_status_history (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  order_id UUID REFERENCES orders(id) ON DELETE CASCADE,
  previous_status TEXT,
  new_status TEXT NOT NULL,
  changed_by UUID REFERENCES users(id),
  reason TEXT,
  changed_at TIMESTAMPTZ DEFAULT NOW()
);

-- ═══════════════════════════════════════
-- CONFIGURACIÓN DEL LOCAL
-- ═══════════════════════════════════════
CREATE TABLE store_config (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  store_name TEXT,
  is_paused BOOLEAN DEFAULT false,
  pickup_enabled BOOLEAN DEFAULT true,
  delivery_enabled BOOLEAN DEFAULT true,
  delivery_cost_type TEXT CHECK (delivery_cost_type IN ('fixed', 'by_zone')) DEFAULT 'fixed',
  delivery_fixed_cost DECIMAL,
  min_order_for_delivery DECIMAL,
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE store_hours (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  store_config_id UUID REFERENCES store_config(id) ON DELETE CASCADE,
  day_of_week INT CHECK (day_of_week BETWEEN 0 AND 6), -- 0=Domingo
  is_open BOOLEAN DEFAULT true,
  open_time_1 TIME,
  close_time_1 TIME,
  open_time_2 TIME,
  close_time_2 TIME
);

CREATE TABLE delivery_zones (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  store_config_id UUID REFERENCES store_config(id) ON DELETE CASCADE,
  name TEXT NOT NULL,
  cost DECIMAL NOT NULL CHECK (cost >= 0),
  enabled BOOLEAN DEFAULT true
);
```

### Relaciones
- `products` → `categories` (N:1)
- `product_variants` → `products` (N:1, CASCADE)
- `order_items` → `orders` (N:1, CASCADE)
- `order_items` → `products` (N:1)
- `order_status_history` → `orders` (N:1, CASCADE)
- `store_hours` → `store_config` (N:1, CASCADE)
- `delivery_zones` → `store_config` (N:1, CASCADE)

### 🔒 Row Level Security (RLS) Policies

```sql
-- CATEGORIES: lectura pública (solo habilitadas), escritura solo admin
ALTER TABLE categories ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee categorías activas" ON categories FOR SELECT USING (enabled = true);
CREATE POLICY "Admin CRUD categorías" ON categories FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');

-- PRODUCTS: lectura pública (solo habilitados + categoría habilitada), escritura solo admin
ALTER TABLE products ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee productos activos" ON products FOR SELECT
  USING (enabled = true AND EXISTS (SELECT 1 FROM categories WHERE categories.id = products.category_id AND categories.enabled = true));
CREATE POLICY "Admin CRUD productos" ON products FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');

-- PRODUCT_VARIANTS: lectura pública, escritura solo admin
ALTER TABLE product_variants ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee variantes" ON product_variants FOR SELECT USING (enabled = true);
CREATE POLICY "Admin CRUD variantes" ON product_variants FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');

-- ORDERS: solo admin puede leer todas, cliente puede insertar
ALTER TABLE orders ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Cualquiera crea pedido" ON orders FOR INSERT WITH CHECK (true);
CREATE POLICY "Admin lee todos los pedidos" ON orders FOR SELECT USING (auth.jwt() ->> 'role' = 'store_admin');
CREATE POLICY "Admin actualiza pedidos" ON orders FOR UPDATE USING (auth.jwt() ->> 'role' = 'store_admin');

-- ORDER_ITEMS: mismo acceso que orders
ALTER TABLE order_items ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Cualquiera inserta items" ON order_items FOR INSERT WITH CHECK (true);
CREATE POLICY "Admin lee items" ON order_items FOR SELECT USING (auth.jwt() ->> 'role' = 'store_admin');

-- ORDER_STATUS_HISTORY: solo admin
ALTER TABLE order_status_history ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Admin gestiona historial" ON order_status_history FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');

-- STORE_CONFIG: lectura pública (para horarios/pausa), escritura solo admin
ALTER TABLE store_config ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee config" ON store_config FOR SELECT USING (true);
CREATE POLICY "Admin edita config" ON store_config FOR UPDATE USING (auth.jwt() ->> 'role' = 'store_admin');

-- STORE_HOURS: lectura pública, escritura admin
ALTER TABLE store_hours ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee horarios" ON store_hours FOR SELECT USING (true);
CREATE POLICY "Admin edita horarios" ON store_hours FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');

-- DELIVERY_ZONES: lectura pública (habilitadas), escritura admin
ALTER TABLE delivery_zones ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Público lee zonas activas" ON delivery_zones FOR SELECT USING (enabled = true);
CREATE POLICY "Admin CRUD zonas" ON delivery_zones FOR ALL USING (auth.jwt() ->> 'role' = 'store_admin');
```

## 🔌 6. API SURFACE (Edge Functions + Client Queries)

### Edge Functions (lógica crítica que NO puede estar solo en el frontend)

| Función | Método | Descripción | Validaciones |
|---|---|---|---|
| `create-order` | POST | Crea un pedido completo | Verifica horarios, modo pausa, productos habilitados, recalcula precios desde DB, valida mínimo de envío, sanitiza inputs, rate limiting (max 5 pedidos/min/IP) |
| `update-order-status` | PATCH | Cambia estado de un pedido | Verifica transición válida, requiere motivo si es cancelación, registra en historial, solo admin autenticado |

### Queries directas desde el frontend (vía Supabase Client)

| Operación | Tabla | Quién | Descripción |
|---|---|---|---|
| `SELECT` | `categories` | Público | Listar categorías habilitadas ordenadas |
| `SELECT` | `products` | Público | Listar productos habilitados por categoría |
| `SELECT` | `product_variants` | Público | Variantes de un producto |
| `SELECT` | `store_config` | Público | Estado de pausa, métodos de entrega |
| `SELECT` | `store_hours` | Público | Horarios del local |
| `SELECT` | `delivery_zones` | Público | Zonas y costos de envío |
| `SELECT` | `orders` | Admin | Bandeja de pedidos con filtros |
| `INSERT/UPDATE/DELETE` | `categories` | Admin | CRUD de categorías |
| `INSERT/UPDATE/DELETE` | `products` | Admin | CRUD de productos |
| `INSERT/UPDATE/DELETE` | `product_variants` | Admin | CRUD de variantes |
| `UPDATE` | `store_config` | Admin | Cambiar pausa, métodos, costos |
| `UPDATE` | `store_hours` | Admin | Editar horarios |
| `INSERT/UPDATE/DELETE` | `delivery_zones` | Admin | CRUD de zonas |

## ⚙️ 7. REGLAS DE NEGOCIO

> *Estas son las "leyes" del sistema que SIEMPRE se deben respetar.*

### Horarios y Disponibilidad
1. **RN-001:** El local tiene horarios configurables por día. Puede ser continuo o cortado. Un día puede estar "cerrado".
2. **RN-002:** Fuera de horario → se permite navegar el catálogo, se **BLOQUEA** el checkout. El backend valida la hora al crear el pedido (doble validación).
3. **RN-003:** El admin puede activar "modo pausa" que cierra la tienda inmediatamente, independiente del horario. Aplican las mismas reglas que fuera de horario.

### Pedidos
4. **RN-010:** Flujo de estados: `Nuevo → En preparación → Listo → Enviado/Retirado → Cerrado`. Cancelación posible desde cualquier estado previo a Cerrado.
5. **RN-011:** Solo se permiten transiciones válidas. El backend rechaza cualquier transición no listada.
6. **RN-012:** Cada cambio de estado genera un registro en `order_status_history` con timestamp, usuario y motivo.
7. **RN-013:** Cancelar un pedido **requiere motivo** obligatorio (min 5 caracteres). Es irreversible.
8. **RN-014:** En F1, solo el admin puede cancelar pedidos. El cliente contacta por WhatsApp.

### Precios y Totales
9. **🔴 RN-020 (REGLA DE ORO):** El **BACKEND es la fuente de verdad** de precios. NUNCA confiar en precios enviados desde el cliente. El backend busca cada producto, verifica que esté habilitado, obtiene el precio actual, aplica variantes, calcula subtotal y total.
10. **RN-021:** Cada `order_item` guarda **snapshots** de nombre y precio al momento de la compra. Cambios posteriores de precio no afectan pedidos existentes.
11. **RN-022:** Productos con `enabled = false` no aparecen en catálogo y no se pueden pedir. Si se pausa mientras está en el carrito, el backend rechaza al confirmar.

### Entrega
12. **RN-030:** Dos métodos: retiro en local (sin costo) y envío a domicilio (con costo según config). El admin habilita/deshabilita cada uno.
13. **RN-031:** Costo de envío: fijo (un monto único) o por zona (selector en checkout). SIN cálculo por GPS/distancia en F1.
14. **RN-032:** Pedido mínimo para envío configurable. Si no alcanza, se bloquea la opción de envío.
15. **RN-033:** Datos obligatorios para envío: dirección + barrio/zona + teléfono.

### Productos
16. **RN-040:** Productos organizados en categorías (1 producto = 1 categoría). Orden configurable.
17. **RN-041:** Flag `enabled` en productos y categorías. Categoría deshabilitada oculta todos sus productos.
18. **RN-042:** Variantes simples con delta de precio (positivo, negativo o cero). Precio final = base + delta.

### Usuarios y Seguridad
19. **RN-050:** Dos roles: `customer` (no requiere login en F1, solo nombre + teléfono) y `store_admin` (login con email + password).
20. **RN-051:** Passwords hasheados con bcrypt. JWT con expiración (8h). Rate limiting en login (5 intentos/min/IP). Todas las rutas admin protegidas por middleware.

### Pagos
21. **RN-060:** F1 solo acepta: efectivo al recibir/retirar + transferencia bancaria (gestión manual). Sin validación automática de pago.
22. **RN-061:** MercadoPago se integra en Fase 1.5. El campo `payment_status` ya existe pero no se usa activamente en F1.

### Datos y Privacidad
23. **RN-070:** Datos mínimos del cliente: nombre (obligatorio) + teléfono (obligatorio) + dirección/zona (solo si envío). No se pide email ni DNI en F1.
24. **RN-071:** Los datos operativos son propiedad del cliente (dueño del local). Tiene derecho a exportarlos.

### Seguridad Avanzada
25. **� RN-080:** Todo input del usuario debe ser **sanitizado** antes de guardarse (prevención de XSS). Usar `sanitizeInput()` de `/utils/sanitizeInput.js` que hace strip de HTML tags y caracteres peligrosos.
26. **RN-081:** Rate limiting en `create-order`: máximo 5 pedidos por minuto por IP. Evita spam y abuso.
27. **RN-082:** Headers de seguridad obligatorios en Vercel: `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `Strict-Transport-Security` (HSTS).
28. **RN-083:** CORS configurado en Supabase: solo aceptar requests desde el dominio propio y las apps nativas (Capacitor).
29. **RN-084:** Los tokens JWT nunca se almacenan en `localStorage` abierto. Se usa `httpOnly` cookies donde sea posible, o Supabase Auth (que maneja esto internamente).
30. **RN-085:** Logging centralizado: toda acción del admin (crear producto, cambiar estado de pedido, modificar config) se registra con timestamp y usuario.

## �🛒 8. FLUJO DE CHECKOUT (Diagrama)

```
┌─────────────────────────────────────────────────────────────────┐
│                     FLUJO DE COMPRA - CLIENTE                   │
└─────────────────────────────────────────────────────────────────┘

1. CATÁLOGO
   Cliente navega categorías → ve productos con precio e imagen
   ↓
2. AGREGAR AL CARRITO
   Selecciona producto → elige variante (si tiene) → agrega observación (opcional) → suma al carrito
   ↓ (el carrito se guarda en localStorage)
3. REVISAR CARRITO (drawer lateral o página)
   Ve items, cantidades, subtotal → puede modificar cantidades o eliminar items
   ↓
4. CHECKOUT
   ├─ 4a. VERIFICACIÓN DE HORARIO
   │     ¿Tienda abierta y no pausada? → SI: continúa  /  NO: muestra banner y bloquea
   ├─ 4b. DATOS PERSONALES
   │     Nombre (obligatorio) + Teléfono (obligatorio)
   ├─ 4c. MÉTODO DE ENTREGA
   │     Retiro en local  vs  Envío a domicilio
   │     Si envío: dirección + zona (si aplica) + referencias
   │     Valida pedido mínimo para envío
   ├─ 4d. MÉTODO DE PAGO
   │     Efectivo  /  Transferencia (F1 solo estos)
   └─ 4e. RESUMEN FINAL
         Muestra: items + subtotal + costo envío + total → botón "Confirmar Pedido"
   ↓
5. BACKEND (Edge Function: create-order)
   ├─ Verifica horarios y pausa (RN-002, RN-003)
   ├─ Busca cada producto en DB, verifica enabled (RN-022)
   ├─ Recalcula precios desde DB, NO usa precios del cliente (RN-020)
   ├─ Guarda snapshots de nombre/precio (RN-021)
   ├─ Calcula subtotal + envío + total
   ├─ Crea orden con status = 'new'
   ├─ Registra en order_status_history
   └─ Retorna order_number
   ↓
6. CONFIRMACIÓN
   Pantalla de confirmación con número de pedido + resumen
   Opción de copiar número o compartir por WhatsApp
```

## 🎨 9. DESIGN TOKENS

### Paleta de Colores
```js
// tailwind.config.js → theme.extend.colors
colors: {
  primary:    { 50: '#f0fdf4', 100: '#dcfce7', 500: '#22c55e', 600: '#16a34a', 700: '#15803d' },  // Verde — acción principal, CTAs
  secondary:  { 50: '#fffbeb', 100: '#fef3c7', 500: '#f59e0b', 600: '#d97706' },                   // Ámbar — acentos, badges
  neutral:    { 50: '#fafafa', 100: '#f5f5f5', 200: '#e5e5e5', 500: '#737373', 800: '#262626', 900: '#171717' },
  danger:     { 500: '#ef4444', 600: '#dc2626' },                                                    // Rojo — errores, cancelar
  success:    { 500: '#22c55e' },                                                                     // Verde — confirmaciones
  info:       { 500: '#3b82f6' }                                                                      // Azul — información
}
```

### Tipografía
```js
// Google Fonts: Inter (UI general) + Outfit (títulos/logo)
fontFamily: {
  sans: ['Inter', 'system-ui', 'sans-serif'],
  display: ['Outfit', 'Inter', 'sans-serif']
}
```

### Bordes y Sombras
```js
borderRadius: { DEFAULT: '0.75rem', sm: '0.5rem', full: '9999px' }
boxShadow: {
  card: '0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)',
  modal: '0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04)'
}
```

### Estilo General
- **Estética:** Limpia, moderna, amigable. Sin sobrecargar. Colores suaves con acentos vibrantes.
- **Tarjetas de producto:** Imagen arriba, nombre + precio, fondo blanco, borde sutil, sombra suave.
- **Botones:** Redondeados (`rounded-xl`), con transición de hover. Primario = verde, Secundario = outline, Danger = rojo.
- **Espaciado:** Generoso. No apretar contenido. Padding mínimo `p-4` en cards, `p-6` en secciones.

## 🚨 10. MANEJO DE ERRORES

### Frontend
| Tipo de error | Componente | Comportamiento |
|---|---|---|
| Error de red / Supabase caído | `Toast` (posición top-right) | "Error de conexión. Intentá de nuevo." + botón Reintentar |
| Producto no disponible al confirmar | `Toast` + resaltar item | "El producto [X] ya no está disponible" + quitar del carrito |
| Fuera de horario al confirmar | `Modal` bloqueante | "La tienda está cerrada. Horario: [X]" |
| Pedido mínimo no alcanzado | Texto inline en checkout | "El pedido mínimo para envío es $[X]. Te faltan $[Y]" |
| Campo obligatorio vacío | Borde rojo + texto debajo | "Este campo es obligatorio" |
| Error desconocido | `Toast` error | "Ocurrió un error inesperado. Contacta al local por WhatsApp." |

### Backend (Edge Functions)
| Situación | HTTP Status | Respuesta |
|---|---|---|
| Producto deshabilitado | 400 | `{ error: "PRODUCT_UNAVAILABLE", product: "nombre" }` |
| Tienda cerrada / pausada | 400 | `{ error: "STORE_CLOSED", message: "..." }` |
| Transición de estado inválida | 400 | `{ error: "INVALID_TRANSITION", from: "X", to: "Y" }` |
| Cancelación sin motivo | 400 | `{ error: "REASON_REQUIRED" }` |
| Rate limit excedido | 429 | `{ error: "RATE_LIMIT_EXCEEDED", retryAfter: 60 }` |
| Input con contenido malicioso | 400 | `{ error: "INVALID_INPUT", field: "nombre_campo" }` |
| No autenticado (admin) | 401 | `{ error: "UNAUTHORIZED" }` |
| Error interno | 500 | `{ error: "INTERNAL_ERROR" }` (log completo en Supabase) |

### Patrón de implementación
```jsx
// Todos los fetch/mutaciones deben usar este patrón:
try {
  const { data, error } = await supabase.from('table').select();
  if (error) throw error;
  return data;
} catch (err) {
  toast.error(getErrorMessage(err)); // Función centralizada en utils/
  console.error('[NombreHook]', err);
}
```

## 💻 11. PROTOCOLO DE CODIFICACIÓN

### Convenciones de Nombres
| Elemento | Formato | Ejemplo |
|---|---|---|
| Tablas SQL | `snake_case` | `order_items`, `store_config` |
| Columnas SQL | `snake_case` | `customer_name`, `created_at` |
| Componentes React | `PascalCase` | `ProductCard.jsx`, `CartDrawer.jsx` |
| Archivos de componentes | `PascalCase.jsx` | `OrderStatusBadge.jsx` |
| Hooks | `camelCase` con prefijo `use` | `useCart.js`, `useStoreConfig.js` |
| Funciones / variables JS | `camelCase` | `calculateTotal`, `isStoreOpen` |
| Constantes | `UPPER_SNAKE_CASE` | `MAX_LOGIN_ATTEMPTS`, `ORDER_STATUSES` |
| Archivos de utils | `camelCase.js` | `formatCurrency.js`, `validateOrder.js` |
| CSS classes (Tailwind) | utility classes | `className="bg-primary-500 text-white rounded-xl"` |

### Reglas de Código
1. **Idioma:** Comentarios y documentación en **Español**. Variables y funciones en **Inglés**.
2. **Arquitectura:** Código modular. Componentes pequeños y reutilizables (max ~150 líneas).
3. **Seguridad:** Validar siempre en el servidor (Edge Functions + RLS), no solo en el cliente.
4. **No Suposiciones:** Si algo entra en conflicto con las Reglas de Negocio (Punto 7), **detente y pregunta**.
5. **Clean Code:** Principios SOLID y DRY.
6. **Snapshots:** Toda información de precio/nombre en pedidos es un snapshot, nunca referencia viva.
7. **Validación doble:** Toda regla crítica (horarios, precios, estados) se valida en frontend Y backend.
8. **Mobile-first:** Diseñar primero para móvil y adaptar a desktop.
9. **Datos:** No hacer fetch en componentes directamente. Usar custom hooks (`useProducts`, `useOrders`, etc.).
10. **Estado del carrito:** Se guarda en `localStorage` + Context. No en Supabase (el cliente no tiene login en F1).
11. **Sanitización:** Todo input de texto del usuario pasa por `sanitizeInput()` antes de enviarse al backend.
12. **Capacitor-aware:** Al usar APIs del dispositivo (push, cámara, etc.), siempre verificar si está disponible (`Capacitor.isNativePlatform()`) y tener un fallback web.

## 🚫 12. LO QUE NO SE DEBE HACER

1. ❌ **No usar `any` en TypeScript** — si se usa TS, tipar todo correctamente.
2. ❌ **No hacer fetch directo en componentes** — siempre usar custom hooks del directorio `/hooks`.
3. ❌ **No crear tablas sin RLS policies** — toda tabla nueva debe tener policies definidas.
4. ❌ **No confiar en datos del frontend para cálculos de precio** — siempre recalcular en backend.
5. ❌ **No guardar contraseñas en texto plano** — siempre bcrypt.
6. ❌ **No crear archivos fuera de la estructura de carpetas definida** — consultar primero.
7. ❌ **No hardcodear valores** — usar variables de entorno (`.env.local`) o constantes con nombre descriptivo.
8. ❌ **No omitir estados de loading/error** — todo fetch debe manejar: loading, success, error.
9. ❌ **No instalar dependencias sin consultar** — preguntar antes de agregar un paquete nuevo.
10. ❌ **No alterar el esquema de base de datos sin consultar** — cambios de schema se discuten antes.
11. ❌ **No guardar inputs del usuario sin sanitizar** — siempre usar `sanitizeInput()` para prevenir XSS.
12. ❌ **No exponer datos sensibles en logs del frontend** — nunca loggear tokens, passwords ni datos personales en `console.log`.
13. ❌ **No asumir que estamos en web** — siempre verificar plataforma antes de usar APIs nativas de Capacitor.
14. ❌ **No desplegar sin verificar headers de seguridad** — comprobar CSP, HSTS, X-Frame-Options antes de cada deploy.

## 🧪 13. DATOS DE PRUEBA (Seed)

```sql
-- ═══ CATEGORÍAS ═══
INSERT INTO categories (id, name, display_order, enabled) VALUES
  ('cat-001', 'Comidas Preparadas', 1, true),
  ('cat-002', 'Helados', 2, true),
  ('cat-003', 'Mercadería', 3, true),
  ('cat-004', 'Alfajores y Golosinas', 4, true);

-- ═══ PRODUCTOS ═══
INSERT INTO products (id, category_id, name, description, price, enabled, display_order) VALUES
  -- Comidas
  ('prod-001', 'cat-001', 'Milanesa napolitana', 'Con jamón, queso y salsa', 4500, true, 1),
  ('prod-002', 'cat-001', 'Empanadas (docena)', 'Carne, pollo o jamón y queso', 6000, true, 2),
  ('prod-003', 'cat-001', 'Tarta de jamón y queso', 'Porción individual', 2500, true, 3),
  ('prod-004', 'cat-001', 'Pizza muzzarella', 'Grande, 8 porciones', 5000, true, 4),
  -- Helados
  ('prod-005', 'cat-002', 'Helado 1/4 kg', 'Elegí hasta 2 gustos', 3000, true, 1),
  ('prod-006', 'cat-002', 'Helado 1/2 kg', 'Elegí hasta 3 gustos', 5200, true, 2),
  ('prod-007', 'cat-002', 'Helado 1 kg', 'Elegí hasta 4 gustos', 9500, true, 3),
  -- Mercadería
  ('prod-008', 'cat-003', 'Coca-Cola 1.5L', NULL, 2200, true, 1),
  ('prod-009', 'cat-003', 'Agua mineral 500ml', NULL, 800, true, 2),
  ('prod-010', 'cat-003', 'Pan lactal', NULL, 1800, true, 3),
  -- Alfajores
  ('prod-011', 'cat-004', 'Alfajor Havanna', 'Chocolate', 1500, true, 1),
  ('prod-012', 'cat-004', 'Alfajor Cachafaz', 'Triple, dulce de leche', 1200, true, 2);

-- ═══ VARIANTES ═══
INSERT INTO product_variants (product_id, name, price_delta) VALUES
  ('prod-002', 'Carne', 0),
  ('prod-002', 'Pollo', 0),
  ('prod-002', 'Jamón y queso', 0),
  ('prod-001', 'Con papas fritas', 1500),
  ('prod-001', 'Con ensalada', 800);

-- ═══ CONFIG DEL LOCAL ═══
INSERT INTO store_config (id, store_name, is_paused, pickup_enabled, delivery_enabled, delivery_cost_type, delivery_fixed_cost, min_order_for_delivery)
VALUES ('config-001', 'Tienda Fran', false, true, true, 'by_zone', NULL, 3000);

-- ═══ HORARIOS ═══
INSERT INTO store_hours (store_config_id, day_of_week, is_open, open_time_1, close_time_1, open_time_2, close_time_2) VALUES
  ('config-001', 0, false, NULL, NULL, NULL, NULL),       -- Domingo cerrado
  ('config-001', 1, true, '09:00', '13:00', '17:00', '21:00'),  -- Lunes cortado
  ('config-001', 2, true, '09:00', '13:00', '17:00', '21:00'),  -- Martes cortado
  ('config-001', 3, true, '09:00', '13:00', '17:00', '21:00'),  -- Miércoles
  ('config-001', 4, true, '09:00', '13:00', '17:00', '21:00'),  -- Jueves
  ('config-001', 5, true, '09:00', '13:00', '17:00', '21:00'),  -- Viernes
  ('config-001', 6, true, '09:00', '14:00', NULL, NULL);         -- Sábado continuo

-- ═══ ZONAS DE ENVÍO ═══
INSERT INTO delivery_zones (store_config_id, name, cost, enabled) VALUES
  ('config-001', 'Centro', 500, true),
  ('config-001', 'Barrio Norte', 700, true),
  ('config-001', 'Barrio Sur', 700, true),
  ('config-001', 'Zona Industrial', 1000, true);

-- ═══ ADMIN ═══
INSERT INTO users (email, password_hash, role, full_name, phone) VALUES
  ('admin@tiendafran.com', '$2b$10$HASH_PLACEHOLDER', 'store_admin', 'Fran (Admin)', '11-1234-5678');
```

## � 14. SEGURIDAD E INFRAESTRUCTURA

### Headers de Seguridad (configurar en Vercel + `vercel.json`)
```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "X-XSS-Protection", "value": "1; mode=block" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" },
        { "key": "Strict-Transport-Security", "value": "max-age=63072000; includeSubDomains; preload" },
        { "key": "Content-Security-Policy", "value": "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' https://*.supabase.co data:; connect-src 'self' https://*.supabase.co" }
      ]
    }
  ]
}
```

### Sanitización de Inputs
```js
// utils/sanitizeInput.js
// Usar en TODOS los inputs de texto del usuario antes de enviar al backend
export function sanitizeInput(input) {
  if (typeof input !== 'string') return input;
  return input
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#x27;')
    .trim();
}

// Validar longitudes máximas
export const INPUT_LIMITS = {
  customerName: 100,
  customerPhone: 20,
  deliveryAddress: 200,
  deliveryNotes: 500,
  itemNotes: 200,
  cancellationReason: 500,
};
```

### Rate Limiting (en Edge Functions)
```js
// Implementar con Supabase o Redis
// create-order: max 5 pedidos/min/IP
// login: max 5 intentos/min/IP (ya definido en RN-051)
// Respuesta cuando se excede: HTTP 429 + { error: "RATE_LIMIT_EXCEEDED", retryAfter: 60 }
```

### Backup y Recuperación
| Concepto | Detalle |
|---|---|
| **Backups automáticos** | Supabase Pro incluye backups diarios automáticos |
| **RPO (Recovery Point Objective)** | Máximo 24 horas de pérdida de datos |
| **RTO (Recovery Time Objective)** | Restauración en menos de 4 horas |
| **Backup manual** | Exportación semanal de datos críticos (pedidos, productos, clientes) en formato CSV como respaldo adicional |
| **Punto de restauración** | Ante desastre, se restaura el último backup de Supabase y se re-deploya desde el último commit estable en Git |

### Monitoreo y Alertas
| Qué monitorear | Herramienta | Alerta |
|---|---|---|
| App caída (web) | Vercel Dashboard + UptimeRobot (tier gratuito) | Email inmediato si la web no responde |
| Errores 500 recurrentes | Supabase Logs + Edge Function logs | Revisar diariamente en los primeros meses |
| Base de datos llena | Supabase Dashboard | Alerta cuando uso > 80% del plan |
| Pedidos sin atender > 15 min | Query automática (cron o Supabase webhook) | Notificación push al admin |
| Login fallidos masivos | Logs de Supabase Auth | Posible intento de acceso no autorizado |

### CORS (configurar en Supabase)
- Permitir orígenes: dominio propio (`https://tiendafran.com`), `localhost:5173` (dev), `capacitor://localhost` (iOS), `http://localhost` (Android)
- Métodos permitidos: `GET, POST, PATCH, DELETE, OPTIONS`
- Headers permitidos: `Authorization, Content-Type, apikey`

---

## �🚀 15. TAREA INICIAL: VALIDACIÓN LÓGICA
Antes de empezar a escribir código, necesito que realices lo siguiente:
1. Analiza la Arquitectura de Datos, las RLS Policies y las Reglas de Negocio proporcionadas.
2. Revisa las medidas de seguridad (headers, sanitización, rate limiting, CORS) y confirma que son adecuadas.
3. Identifica posibles "casos de borde" (edge cases) o inconsistencias que no hayamos previsto.
4. Confirma que entiendes el stack (incluyendo Capacitor), la estructura de carpetas y la lógica.

**No generes código hasta que yo te dé el "OK" tras tu análisis.**

---
**Infinite Solutions** | *Desarrollo de Software de Alto Nivel*.
