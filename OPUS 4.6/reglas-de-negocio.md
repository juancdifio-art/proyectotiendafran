# Reglas de Negocio - Fase 1
## Sistema de Pedidos: Tienda Fran

**Fecha:** 2026-02-09
**Estado:** borrador pre-Discovery (se cierra formalmente despues del relevamiento)
**Audiencia:** equipo de desarrollo + cliente

---

## 1. Horarios y Disponibilidad

### RN-001: Horarios de apertura/cierre
- El local tiene horarios configurables por dia de la semana.
- Cada dia puede tener un horario continuo (ej: 9:00-21:00) o cortado (ej: 9:00-13:00 y 17:00-21:00).
- Un dia puede marcarse como "cerrado" (no acepta pedidos en todo el dia).
- Los horarios se configuran desde el panel admin por el administrador del local.

### RN-002: Fuera de horario = no se aceptan pedidos
- Si el local esta fuera del horario configurado, el sistema:
  - Muestra un banner informativo: "Estamos cerrados. Nuestro horario: [horario del dia siguiente]"
  - Permite navegar el catalogo normalmente
  - **Bloquea** el boton de checkout / confirmar pedido
- El backend valida la hora al crear el pedido (doble validacion, no solo frontend).

### RN-003: Pausa manual
- El admin puede activar un "modo pausa" que cierra la tienda inmediatamente, independientemente del horario configurado.
- Razones tipicas: falta de stock, emergencia, fin del turno anticipado, exceso de pedidos.
- La pausa se desactiva manualmente desde el panel.
- Mientras esta pausada, aplican las mismas reglas que fuera de horario (RN-002).

### RN-004: Excepcion futura - pedido programado
- En Fase 1 **no** se permite hacer pedidos para horarios futuros.
- Esta funcionalidad se evalua para F1.5 o F2.
- **Decision Discovery:** confirmar si el cliente necesita pedidos programados para mayorista.

---

## 2. Pedidos

### RN-010: Estados del pedido
Los pedidos siguen un flujo lineal con posibilidad de cancelacion:

```
Nuevo -> En preparacion -> Listo -> Enviado/Retirado -> Cerrado
```

Flujo alternativo:
```
[Cualquier estado previo a Cerrado] -> Cancelado
```

| Estado | Significado | Quien lo activa |
|---|---|---|
| Nuevo | Pedido recibido, pendiente de revision | Sistema (al crear) |
| En preparacion | Admin acepto y se esta preparando | Admin |
| Listo | Pedido terminado, esperando entrega o retiro | Admin |
| Enviado | Se despacho para delivery | Admin |
| Retirado | El cliente lo retiro en el local | Admin |
| Cerrado | Pedido completado exitosamente | Admin |
| Cancelado | Pedido cancelado por el admin (con motivo) | Admin |

### RN-011: Transiciones validas
- `Nuevo` -> `En preparacion` o `Cancelado`
- `En preparacion` -> `Listo` o `Cancelado`
- `Listo` -> `Enviado` (si delivery) o `Retirado` (si retiro) o `Cancelado`
- `Enviado` -> `Cerrado`
- `Retirado` -> `Cerrado`
- `Cerrado` -> no se puede cambiar (estado final)
- `Cancelado` -> no se puede cambiar (estado final)

Cualquier transicion no listada arriba es **invalida** y el backend la rechaza.

### RN-012: Registro de cambios de estado
- Cada cambio de estado genera un registro en `order_status_history` con:
  - Estado anterior y nuevo
  - Timestamp exacto
  - Usuario que hizo el cambio
  - Motivo (obligatorio en cancelacion, opcional en otros cambios)

### RN-013: Cancelacion requiere motivo
- Para cancelar un pedido, el admin debe ingresar un motivo (texto corto, minimo 5 caracteres).
- El motivo queda registrado y es visible en el historial del pedido.
- Cancelar es irreversible.

### RN-014: El cliente no puede cancelar pedidos en F1
- En Fase 1, solo el admin puede cancelar pedidos.
- El cliente puede contactar por WhatsApp si necesita cancelar.
- **Decision Discovery:** evaluar si se agrega cancelacion por parte del cliente (con restriccion de tiempo, ej: dentro de los primeros 2 minutos).

---

## 3. Precios y Totales

### RN-020: Backend es la fuente de verdad
- Al crear un pedido (`POST /orders`), el backend:
  1. Recibe la lista de items del carrito (product_id, quantity, variant_id, observaciones)
  2. Busca cada producto en la base de datos
  3. Verifica que este habilitado (`enabled = true`)
  4. Obtiene el precio actual y, si tiene variante, aplica el delta
  5. Calcula subtotal: suma de (precio * cantidad) de cada item
  6. Calcula costo de envio segun configuracion y metodo elegido
  7. Calcula total: subtotal + envio
  8. Guarda **snapshots** de nombre y precio en cada `order_item`
- **Nunca** se confia en los precios o totales enviados desde el cliente.

### RN-021: Snapshots de precio
- Cada `order_item` guarda:
  - `product_name_snapshot`: nombre del producto al momento de la compra
  - `product_price_snapshot`: precio unitario al momento de la compra
  - `variant_snapshot`: nombre y delta de la variante (si aplica)
- Si el admin cambia el precio de un producto despues, los pedidos existentes mantienen el precio original.

### RN-022: Productos pausados no se pueden pedir
- Si un producto tiene `enabled = false`, no aparece en el catalogo y no se puede incluir en un pedido.
- Si un producto se pausa mientras un cliente lo tiene en el carrito, al intentar confirmar el pedido, el backend rechaza con error descriptivo: "El producto [nombre] ya no esta disponible".

---

## 4. Entrega

### RN-030: Metodos de entrega
- El sistema soporta dos metodos:
  - **Retiro en local:** el cliente retira personalmente. No tiene costo adicional.
  - **Envio a domicilio:** el local despacha al cliente. Tiene costo segun configuracion.
- El admin puede habilitar/deshabilitar cada metodo desde Configuracion.
- Si solo hay un metodo habilitado, el checkout lo preselecciona automaticamente.

### RN-031: Costo de envio
El costo de envio se calcula segun la configuracion del admin:

| Tipo | Descripcion |
|---|---|
| **Fijo** | Un monto unico para todos los envios (ej: $500) |
| **Por zona** | Lista de zonas con costo asociado. El cliente selecciona su zona en el checkout. |

- En Fase 1 **no** hay calculo por distancia/radio ni por GPS.
- **Decision Discovery:** definir con el cliente cuantas zonas y que costos.

### RN-032: Pedido minimo para envio (opcional)
- El admin puede configurar un monto minimo de pedido para habilidar envio (ej: $2,000).
- Si el subtotal no alcanza el minimo, el checkout:
  - Muestra mensaje: "El pedido minimo para envio es de $[monto]. Te faltan $[diferencia]"
  - Bloquea la opcion de envio (retiro sigue disponible si esta habilitado)
- Si no se configura minimo, no hay restriccion.

### RN-033: Datos requeridos para envio
Si el cliente elige envio a domicilio, debe completar:
- Direccion (calle y numero) - **obligatorio**
- Barrio/Zona - **obligatorio** (selector si es por zona, texto libre si es fijo)
- Referencias (ej: "casa amarilla, portón negro") - **opcional**
- Telefono ya es obligatorio en todos los casos

---

## 5. Productos y Catalogo

### RN-040: Estructura del catalogo
- Los productos se organizan en categorias.
- Cada producto pertenece a exactamente una categoria.
- Las categorias tienen un orden configurable para el catalogo.

### RN-041: Habilitado/Pausado
- Tanto productos como categorias tienen un flag `enabled`.
- Producto con `enabled = false` no aparece en el catalogo ni se puede pedir.
- Categoria con `enabled = false` oculta todos sus productos del catalogo (no importa si los productos estan habilitados individualmente).

### RN-042: Variantes simples
- Un producto puede tener 0 o mas variantes (ej: tamano chico/mediano/grande).
- Cada variante tiene un nombre y un delta de precio (puede ser positivo, negativo o cero).
- El precio final del producto con variante = precio base + delta de la variante.
- **Decision pendiente:** incluir variantes en F1 o postergar a F1.5.

### RN-043: Imagenes
- Cada producto puede tener una imagen.
- Las imagenes se almacenan en servicio externo (Cloudinary o Supabase Storage).
- En la base de datos solo se guarda la URL de la imagen.
- Si un producto no tiene imagen, se muestra un placeholder generico.

---

## 6. Usuarios y Autenticacion

### RN-050: Roles en Fase 1
| Rol | Acceso | Notas |
|---|---|---|
| `customer` | Catalogo, carrito, checkout, seguimiento de pedido | No requiere login en F1 |
| `store_admin` | Panel admin completo | Login con email + password |

- En F1 los clientes **no** necesitan crear cuenta. Solo ingresan nombre y telefono al hacer un pedido.
- **Decision Discovery:** evaluar si conviene exigir registro para beneficios futuros (historial, reordenar).

### RN-051: Seguridad de admin
- Login con email y password.
- Passwords hasheados con bcrypt (o similar).
- JWT con expiracion (ej: 8 horas).
- Rate limiting en login: maximo 5 intentos por minuto por IP.
- Todas las rutas de admin protegidas por middleware de autenticacion.

---

## 7. Pagos

### RN-060: Metodos de pago en Fase 1
- **Efectivo** al recibir/retirar el pedido.
- **Transferencia bancaria** (el cliente transfiere y avisa al local).
- No hay validacion automatica de pago en F1. El admin gestiona manualmente.

### RN-061: Pagos online (futuro)
- MercadoPago se evalua para Fase 1.5.
- La arquitectura del pedido ya contempla un campo `payment_status` para uso futuro, pero en F1 no se utiliza activamente.

---

## 8. Datos y Privacidad

### RN-070: Datos minimos del cliente
Al hacer un pedido, se solicitan:
- Nombre - obligatorio
- Telefono - obligatorio
- Direccion (solo si elige envio) - obligatorio para envio
- Barrio/zona (solo si elige envio) - obligatorio para envio
- No se solicita email ni DNI en F1.

### RN-071: Propiedad de datos
- Los datos operativos (clientes, pedidos, catalogo) son propiedad del cliente (dueño del local).
- El cliente tiene derecho a exportar sus datos en formato acordado.

---

## 9. Reglas Pendientes de Definir en Discovery

| # | Regla | Pregunta clave | Impacto |
|---|---|---|---|
| 1 | Menu variable | El menu de comidas preparadas cambia por dia? | Complejidad de CRUD y UX |
| 2 | Helados especiales | Hay restricciones de horario/zona para envio de helados? | Reglas de checkout |
| 3 | Stock visible | El cliente ve cantidad disponible o solo "disponible/no disponible"? | UI del catalogo |
| 4 | Horario cortado | El local tiene horario cortado (mediodia y noche)? | Configuracion de horarios |
| 5 | Limites de pedido | Hay un maximo de items o monto por pedido? | Validaciones |
| 6 | Zonas de entrega | Cuantas zonas hay y cuanto cuesta cada una? | Config de envio |
| 7 | Pedido minimo | Existe un monto minimo? Cual? | Validacion de checkout |
| 8 | Descuentos en F1 | Se necesita algun descuento basico (ej: 2x1 en alfajores)? | Complejidad de pricing |

---

*Documento borrador. Se cierra formalmente con el cliente durante la fase de Discovery.*
