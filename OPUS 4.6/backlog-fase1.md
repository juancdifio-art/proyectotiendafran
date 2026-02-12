# Backlog Fase 1 - MVP Single-Store
## Historias de Usuario y Tickets de Desarrollo

**Proyecto:** Sistema de Pedidos - Tienda Fran
**Fase:** 1 - MVP
**Fecha:** 2026-02-09
**Estado:** borrador para revision interna

---

## Convenciones

- **Prioridad:** P0 = blocker (sin esto no se lanza), P1 = importante, P2 = deseable
- **Estimacion:** en story points (1=trivial, 2=simple, 3=medio, 5=complejo, 8=muy complejo)
- **Criterios de aceptacion (CA):** condiciones que deben cumplirse para dar el ticket como terminado

---

## Epic 1: Infraestructura y Setup

### US-001: Setup del proyecto y entorno de desarrollo
**Prioridad:** P0 | **Estimacion:** 3

**Como** desarrollador
**Quiero** tener el proyecto inicializado con el stack definido
**Para** poder empezar a desarrollar funcionalidades

**Tareas:**
- [ ] Inicializar proyecto (Next.js / Astro segun decision)
- [ ] Configurar TypeScript, ESLint, Prettier
- [ ] Configurar Tailwind CSS
- [ ] Inicializar Prisma con PostgreSQL
- [ ] Configurar variables de entorno (.env.example)
- [ ] Configurar repositorio Git con .gitignore adecuado
- [ ] Documentar instrucciones de setup local en README

**CA:**
- El proyecto arranca localmente sin errores
- Prisma conecta a la base de datos
- Existe .env.example con todas las variables necesarias

---

### US-002: Modelo de base de datos inicial
**Prioridad:** P0 | **Estimacion:** 5

**Como** desarrollador
**Quiero** tener el modelo de datos creado y migrado
**Para** que todas las entidades principales esten disponibles

**Tareas:**
- [ ] Crear schema de Prisma con todas las entidades de F1:
  - `stores`, `users`, `categories`, `products`, `product_variants`
  - `orders`, `order_items`, `order_status_history`, `store_settings`
- [ ] Incluir `store_id` en toda entidad principal (multi-store ready)
- [ ] Crear migracion inicial
- [ ] Crear seed con datos de prueba (1 store, categorias, productos de ejemplo)
- [ ] Documentar modelo de datos

**CA:**
- `npx prisma migrate dev` ejecuta sin errores
- `npx prisma db seed` genera datos de prueba navegables
- Todas las relaciones (FK) estan correctas

---

### US-003: Autenticacion de admin
**Prioridad:** P0 | **Estimacion:** 5

**Como** admin del local
**Quiero** poder logearme de forma segura al panel
**Para** que solo yo pueda gestionar pedidos y productos

**Tareas:**
- [ ] Endpoint `POST /auth/admin/login` (email + password)
- [ ] Generacion de JWT con role `store_admin` y `store_id`
- [ ] Middleware de autenticacion para rutas protegidas
- [ ] Middleware de autorizacion por rol
- [ ] Rate limiting en endpoint de login (max 5 intentos por minuto)
- [ ] UI de login para el panel admin

**CA:**
- Admin puede loguearse con credenciales validas
- Credenciales invalidas devuelven 401 con mensaje generico
- JWT expira en tiempo razonable (ej: 8 horas)
- Rutas /admin/* redirigen a login si no hay sesion valida
- Despues de 5 intentos fallidos, se bloquea temporalmente

---

## Epic 2: Catalogo y Productos

### US-004: Ver catalogo de productos (cliente)
**Prioridad:** P0 | **Estimacion:** 5

**Como** cliente
**Quiero** ver los productos organizados por categoria
**Para** elegir que quiero pedir

**Tareas:**
- [ ] Endpoint `GET /catalog` que devuelve categorias con sus productos habilitados
- [ ] Pagina de catalogo mobile-first con listado por categoria
- [ ] Mostrar por producto: nombre, precio, imagen, disponibilidad
- [ ] Solo mostrar productos con `enabled = true`
- [ ] Solo mostrar categorias con `enabled = true` y que tengan productos activos
- [ ] Ordenar categorias segun campo `order`

**CA:**
- El catalogo carga en menos de 3 segundos en 3G
- Productos pausados no aparecen en el catalogo
- Categorias vacias (sin productos activos) no se muestran
- Las imagenes se cargan de forma lazy

---

### US-005: Ver detalle de producto (cliente)
**Prioridad:** P0 | **Estimacion:** 3

**Como** cliente
**Quiero** ver el detalle de un producto
**Para** decidir si lo agrego al carrito

**Tareas:**
- [ ] Endpoint `GET /products/:id` con variantes activas
- [ ] Pagina de detalle: nombre, descripcion, precio, imagen grande, variantes
- [ ] Selector de variante (si tiene) con ajuste de precio visible
- [ ] Campo de observaciones (texto libre, max 250 chars)
- [ ] Boton "Agregar al carrito"

**CA:**
- La pagina muestra toda la info del producto
- Si tiene variantes, el precio se ajusta al seleccionar
- El campo de observaciones no permite mas de 250 caracteres
- Si el producto no esta habilitado, redirige al catalogo

---

### US-006: CRUD de productos (admin)
**Prioridad:** P0 | **Estimacion:** 5

**Como** admin del local
**Quiero** poder crear, editar y pausar productos
**Para** mantener mi catalogo actualizado

**Tareas:**
- [ ] Endpoint `GET /admin/products` (lista con filtros)
- [ ] Endpoint `POST /admin/products` (crear)
- [ ] Endpoint `PATCH /admin/products/:id` (editar)
- [ ] Endpoint `DELETE /admin/products/:id` (baja logica: enabled=false)
- [ ] UI: Lista de productos con search basico y filtro por categoria
- [ ] UI: Formulario crear/editar producto (nombre, descripcion, precio, categoria, imagen, habilitado)
- [ ] Upload de imagen (Cloudinary o Supabase Storage)
- [ ] Validaciones server-side: nombre requerido, precio > 0, categoria valida

**CA:**
- Admin puede crear un producto con imagen y aparece en el catalogo
- Admin puede editar precio/nombre y se refleja inmediatamente
- Admin puede pausar un producto y desaparece del catalogo publico
- No se pueden crear productos sin nombre o con precio negativo

---

### US-007: CRUD de categorias (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** poder crear, editar y desactivar categorias
**Para** organizar mi catalogo

**Tareas:**
- [ ] Endpoint `GET /admin/categories`
- [ ] Endpoint `POST /admin/categories`
- [ ] Endpoint `PATCH /admin/categories/:id`
- [ ] UI: Lista de categorias con drag-and-drop o flechas para reordenar
- [ ] Validacion: no se puede eliminar categoria con productos activos (solo desactivar)

**CA:**
- Admin puede crear categorias nuevas
- Admin puede reordenar categorias y se refleja en el catalogo
- Desactivar una categoria oculta sus productos en el catalogo
- Error claro si intenta eliminar categoria con productos activos

---

### US-008: Variantes de producto (admin)
**Prioridad:** P1 | **Estimacion:** 5

**Como** admin del local
**Quiero** poder definir variantes simples de un producto (tamano, sabor, pack)
**Para** que el cliente elija la opcion que prefiere

**Tareas:**
- [ ] Endpoint CRUD para `product_variants`
- [ ] UI en formulario de producto: seccion de variantes (nombre + delta de precio)
- [ ] Las variantes aparecen en el detalle de producto del cliente
- [ ] Al agregar al carrito, se guarda la variante seleccionada

**CA:**
- Admin puede agregar variantes con nombre y diferencia de precio
- El precio final se calcula como precio base + delta de la variante
- El carrito muestra la variante seleccionada
- Si el producto no tiene variantes, no se muestra el selector

**Nota:** Si complejiza demasiado F1, se puede postergar a F1.5 (decision pendiente).

---

## Epic 3: Carrito y Checkout

### US-009: Carrito de compras (cliente)
**Prioridad:** P0 | **Estimacion:** 5

**Como** cliente
**Quiero** poder armar mi pedido agregando y quitando productos
**Para** hacer un unico pedido con todo lo que necesito

**Tareas:**
- [ ] Estado del carrito en localStorage (sin necesidad de login)
- [ ] Agregar producto al carrito (con variante y observaciones si aplican)
- [ ] Modificar cantidad de cada item
- [ ] Eliminar item del carrito
- [ ] Ver resumen: lista de items, subtotal, costo de envio (si aplica), total
- [ ] Indicador de cantidad de items en el carrito (badge)
- [ ] Persistencia del carrito entre recargas de pagina

**CA:**
- El carrito persiste al cerrar y abrir el navegador
- Subtotal se calcula correctamente con variantes
- Se puede modificar cantidad entre 1 y un maximo razonable (ej: 99)
- El carrito muestra observaciones de cada item si las tiene

---

### US-010: Checkout y creacion de pedido (cliente)
**Prioridad:** P0 | **Estimacion:** 8

**Como** cliente
**Quiero** completar mis datos y confirmar el pedido
**Para** que el local reciba mi pedido y me lo prepare

**Tareas:**
- [ ] Pagina de checkout con formulario:
  - Nombre (requerido)
  - Telefono (requerido)
  - Metodo de entrega: Retiro en local / Envio a domicilio
  - Si envio: direccion, barrio/zona, referencias
  - Opcion "Lo antes posible" o franja horaria (si se habilita)
- [ ] Validacion client-side y server-side de todos los campos
- [ ] Endpoint `POST /orders`:
  - Recibe items del carrito + datos del cliente
  - Backend busca productos en DB, verifica disponibilidad
  - Recalcula subtotal, costo de envio y total (NUNCA confiar en el cliente)
  - Guarda snapshots de nombre y precio en `order_items`
  - Verifica que el local esta abierto y acepta pedidos
  - Verifica pedido minimo si existe
  - Crea el pedido con estado "Nuevo"
  - Crea registro en `order_status_history`
- [ ] Pagina de confirmacion: "Pedido recibido", ID del pedido, resumen, estado
- [ ] Limpiar carrito despues de confirmacion exitosa

**CA:**
- Si el local esta cerrado o pausado, el checkout bloquea con mensaje claro
- Si un producto fue pausado entre el carrito y el checkout, se informa al cliente
- El total del pedido coincide con el recalculo del backend (no se puede manipular)
- El pedido se crea con estado "Nuevo" y aparece en la bandeja del admin
- Se guardan snapshots correctos de nombre y precio en cada item
- Si existe minimo de envio y no se cumple, se bloquea checkout con mensaje

---

### US-011: Verificar estado del local antes de checkout
**Prioridad:** P0 | **Estimacion:** 3

**Como** cliente
**Quiero** saber si el local esta abierto antes de intentar pedir
**Para** no perder tiempo armando un pedido que no se va a recibir

**Tareas:**
- [ ] Endpoint `GET /store/status` que devuelve estado actual (abierto/cerrado/pausado)
- [ ] Banner visible en la tienda si el local esta cerrado: "Estamos cerrados. Nuestro horario: ..."
- [ ] Bloqueo del boton "Ir al checkout" si el local esta cerrado
- [ ] Doble validacion en el backend al crear pedido

**CA:**
- Si el local esta cerrado, se muestra banner y se bloquea checkout
- Si el local se cierra mientras el cliente tiene el carrito abierto, se bloquea al intentar confirmar
- El estado se actualiza sin necesidad de recargar la pagina (poll cada 60s o similar)

---

### US-012: Consultar estado de pedido (cliente)
**Prioridad:** P1 | **Estimacion:** 3

**Como** cliente
**Quiero** consultar en que estado esta mi pedido
**Para** saber si ya esta listo o en camino

**Tareas:**
- [ ] Endpoint `GET /orders/:id/status` (publico, solo con ID del pedido)
- [ ] Pagina simple de seguimiento: estado actual con descripcion y hora de ultimo cambio
- [ ] Link a esta pagina desde la confirmacion del pedido

**CA:**
- El cliente puede ver el estado actual sin loguearse
- Muestra el estado con texto amigable ("Tu pedido se esta preparando")
- Se actualiza al refrescar la pagina

---

## Epic 4: Gestion de Pedidos (Admin)

### US-013: Bandeja de pedidos (admin)
**Prioridad:** P0 | **Estimacion:** 5

**Como** admin del local
**Quiero** ver todos los pedidos organizados por estado
**Para** saber que tengo que preparar y en que orden

**Tareas:**
- [ ] Endpoint `GET /admin/orders` con filtros por estado y rango de fecha
- [ ] UI: Vista de bandeja con columnas o tabs por estado (Nuevo / En preparacion / Listo / Enviado-Retirado / Cerrado)
- [ ] Cada tarjeta de pedido muestra: ID, hora, nombre cliente, cantidad de items, total, tipo de entrega
- [ ] Ordenar por fecha de creacion (mas viejo primero dentro de cada estado)
- [ ] Indicador visual de pedidos nuevos (highlight o badge)

**CA:**
- Los pedidos aparecen en la columna correcta segun su estado
- Los pedidos nuevos tienen un indicador visual claro
- Se puede filtrar por fecha
- La vista es usable en tablet (no solo desktop)

---

### US-014: Detalle de pedido (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** ver el detalle completo de un pedido
**Para** saber exactamente que preparar y para quien

**Tareas:**
- [ ] Endpoint `GET /admin/orders/:id` con items, observaciones, datos de cliente y historial de estados
- [ ] UI: Vista de detalle con toda la info:
  - Datos del cliente (nombre, telefono, direccion si envio)
  - Lista de items con cantidad, variante, observaciones, precio snapshot
  - Subtotal, costo envio, total
  - Historial de cambios de estado con timestamps
  - Tipo de entrega y datos de delivery

**CA:**
- Se ve toda la informacion necesaria para preparar el pedido
- Las observaciones por item son visibles y resaltadas
- El historial de estados muestra cada cambio con hora

---

### US-015: Cambiar estado de pedido (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** cambiar el estado de un pedido
**Para** llevar el control del progreso de cada pedido

**Tareas:**
- [ ] Endpoint `PATCH /admin/orders/:id/status` con validacion de transiciones validas
- [ ] Botones de accion contextuales segun estado actual:
  - Nuevo -> "Aceptar" (pasa a En preparacion) o "Cancelar"
  - En preparacion -> "Listo"
  - Listo -> "Enviado" (si delivery) o "Retirado" (si retiro)
  - Enviado/Retirado -> "Cerrar"
- [ ] Cada cambio crea registro en `order_status_history` con timestamp y usuario
- [ ] Transiciones invalidas bloqueadas (ej: no se puede pasar de Cerrado a Nuevo)

**CA:**
- Solo aparecen los botones de accion validos para cada estado
- Cada transicion queda registrada en el historial
- No se puede hacer transiciones invalidas (backend las rechaza con 400)

---

### US-016: Cancelar pedido con motivo (admin)
**Prioridad:** P0 | **Estimacion:** 2

**Como** admin del local
**Quiero** cancelar un pedido indicando el motivo
**Para** registrar por que no se pudo completar

**Tareas:**
- [ ] Modal de cancelacion con campo de motivo (texto corto, requerido)
- [ ] Se puede cancelar desde cualquier estado previo a "Cerrado"
- [ ] El motivo se guarda en `order_status_history`

**CA:**
- No se puede cancelar sin motivo
- El motivo queda registrado y visible en el detalle del pedido
- El estado cambia a "Cancelado" y no se puede revertir

---

### US-017: Notificacion de pedido nuevo (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** recibir una alerta cuando entra un pedido nuevo
**Para** no tener que estar mirando la pantalla todo el tiempo

**Tareas:**
- [ ] Sonido de alerta en el panel admin cuando llega un pedido nuevo
- [ ] Polling del panel cada 15-30 segundos para detectar pedidos nuevos
- [ ] Badge con cantidad de pedidos nuevos en la bandeja
- [ ] Notificacion push del navegador (si el usuario acepta permisos)

**CA:**
- Suena una alerta cuando hay un pedido nuevo
- El badge se actualiza automaticamente
- Funciona con el panel abierto en background (tab inactiva)

---

## Epic 5: Configuracion del Local

### US-018: Configurar horarios de atencion (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** configurar los horarios de apertura y cierre por dia
**Para** que la tienda se abra y cierre automaticamente

**Tareas:**
- [ ] Endpoint `PATCH /admin/store/settings` para actualizar horarios
- [ ] UI: Tabla de 7 dias con hora de apertura y cierre para cada uno
- [ ] Opcion de marcar un dia como "cerrado"
- [ ] Soporte para horario cortado (ej: 9-13 y 17-21)
- [ ] El endpoint `GET /store/status` calcula estado actual en base a estos horarios

**CA:**
- Se pueden configurar horarios distintos para cada dia
- Un dia marcado como cerrado no acepta pedidos
- El horario cortado funciona correctamente
- El catalogo muestra "Cerrado" fuera de horario

---

### US-019: Pausa manual del local (admin)
**Prioridad:** P0 | **Estimacion:** 2

**Como** admin del local
**Quiero** pausar los pedidos manualmente
**Para** poder cerrar la tienda en caso de emergencia o razon operativa

**Tareas:**
- [ ] Toggle "Pausar tienda" en el panel admin
- [ ] Cuando activado, override de horarios: la tienda aparece como cerrada
- [ ] Mensaje personalizable: "Estamos cerrados temporalmente" (texto por defecto)
- [ ] El toggle es visible y prominente en el dashboard

**CA:**
- Activar la pausa cierra la tienda inmediatamente independientemente del horario
- El mensaje de pausa se muestra en la tienda
- Desactivar la pausa vuelve al modo normal (horario configurado)

---

### US-020: Configurar opciones de entrega (admin)
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** configurar si ofrezco retiro, envio o ambos, y los costos
**Para** definir como reciben los clientes sus pedidos

**Tareas:**
- [ ] Opciones: retiro habilitado (si/no), envio habilitado (si/no)
- [ ] Tipo de costo de envio: fijo o por zona
- [ ] Si fijo: un monto unico para todos los envios
- [ ] Si por zona: lista simple de zonas con costo asociado (nombre zona + precio)
- [ ] Pedido minimo para envio (opcional, monto configurable)
- [ ] El checkout muestra solo las opciones habilitadas

**CA:**
- Si solo retiro esta habilitado, el checkout no muestra opcion de envio
- El costo de envio se calcula correctamente segun configuracion
- El pedido minimo bloquea el checkout con mensaje claro si no se cumple

---

## Epic 6: UI/UX General

### US-021: Layout mobile-first de la tienda
**Prioridad:** P0 | **Estimacion:** 5

**Como** cliente
**Quiero** que la tienda se vea y funcione bien en mi celular
**Para** poder pedir comodamente desde donde este

**Tareas:**
- [ ] Layout responsivo mobile-first con Tailwind
- [ ] Header con logo/nombre del local, link al carrito con badge
- [ ] Navegacion por categorias (tabs o scroll horizontal)
- [ ] Footer con link de WhatsApp para consultas
- [ ] Sistema de toasts/notificaciones para feedback (item agregado, error, etc)
- [ ] Loading states en todas las vistas que hacen fetch

**CA:**
- La tienda es usable y se ve bien en celulares de 360px+
- El carrito es accesible desde cualquier pagina
- El usuario recibe feedback visual en cada accion (agregar al carrito, error, etc)

---

### US-022: Layout del panel admin
**Prioridad:** P0 | **Estimacion:** 3

**Como** admin del local
**Quiero** un panel de administracion claro y rapido
**Para** gestionar mi operacion sin perder tiempo

**Tareas:**
- [ ] Sidebar con navegacion: Dashboard, Pedidos, Productos, Categorias, Configuracion
- [ ] Dashboard simple: pedidos del dia (cantidad y monto), pedidos pendientes
- [ ] Responsivo: usable en tablet y desktop
- [ ] Protegido por autenticacion (redirect a login si no hay sesion)

**CA:**
- La navegacion entre secciones es rapida y sin recargas
- El dashboard muestra resumen util del dia
- Funciona bien en pantallas de 768px+

---

## Epic 7: Deploy y Salida

### US-023: Deploy a produccion
**Prioridad:** P0 | **Estimacion:** 5

**Como** equipo de desarrollo
**Quiero** tener la aplicacion desplegada en produccion con dominio propio
**Para** que los clientes puedan acceder a la tienda

**Tareas:**
- [ ] Configurar hosting (Vercel / Render / Railway segun decision)
- [ ] Configurar base de datos productiva (PostgreSQL)
- [ ] Configurar dominio y SSL
- [ ] Variables de entorno de produccion
- [ ] Configurar backups diarios automaticos de la DB
- [ ] Monitoreo basico de errores (Sentry o similar)
- [ ] Monitoreo de uptime (UptimeRobot o similar)
- [ ] Pipeline de deploy (push a main = deploy automatico)

**CA:**
- La aplicacion es accesible via HTTPS con dominio propio
- Los backups se ejecutan diariamente y se verifico la restauracion
- Los errores en produccion se capturan y notifican
- El deploy automatico funciona correctamente

---

### US-024: Capacitacion al personal del local
**Prioridad:** P0 | **Estimacion:** 2

**Como** admin del local
**Quiero** saber como usar el sistema
**Para** operar sin depender del equipo tecnico

**Tareas:**
- [ ] Sesion de capacitacion presencial o por videollamada (1-2 horas)
- [ ] Practicar flujo completo: crear producto, recibir pedido, cambiar estados, cerrar
- [ ] Practicar configuracion: horarios, pausa, envio
- [ ] Entregar guia breve de uso (ver US-025)

**CA:**
- El admin puede operar el sistema sin asistencia tecnica
- Se practica al menos un flujo completo en vivo

---

### US-025: Guia breve de uso (admin)
**Prioridad:** P1 | **Estimacion:** 2

**Como** admin del local
**Quiero** una guia escrita de como usar el sistema
**Para** consultarla cuando tenga dudas

**Tareas:**
- [ ] Documento PDF o pagina con capturas de pantalla
- [ ] Secciones: Login, Pedidos, Productos, Categorias, Configuracion
- [ ] Tips y preguntas frecuentes
- [ ] Contacto de soporte

**CA:**
- La guia cubre todas las funciones principales con capturas
- Es comprensible sin conocimiento tecnico

---

## Resumen de Estimacion

| Epic | Tickets | SP Total |
|---|---|---|
| 1. Infraestructura y Setup | US-001 a US-003 | 13 |
| 2. Catalogo y Productos | US-004 a US-008 | 21 |
| 3. Carrito y Checkout | US-009 a US-012 | 19 |
| 4. Gestion de Pedidos (Admin) | US-013 a US-017 | 16 |
| 5. Configuracion del Local | US-018 a US-020 | 8 |
| 6. UI/UX General | US-021 a US-022 | 8 |
| 7. Deploy y Salida | US-023 a US-025 | 9 |
| **TOTAL** | **25 tickets** | **94 SP** |

---

## Orden de Ejecucion Sugerido

```
Semana 3-4: US-001, US-002, US-003 (setup + DB + auth)
Semana 4-5: US-004, US-005, US-006, US-007 (catalogo + CRUD)
Semana 5-6: US-009, US-010, US-011 (carrito + checkout)
Semana 6-7: US-013, US-014, US-015, US-016, US-017 (bandeja admin)
Semana 7:   US-018, US-019, US-020 (config local)
Semana 7-8: US-021, US-022 (UI polish)
Semana 8:   US-008, US-012, US-025 (variantes, seguimiento, guia)
Semana 9:   US-023, US-024 (deploy + capacitacion)
```

---

*Este backlog es un borrador para revision interna. Se ajusta con los resultados del Discovery.*
