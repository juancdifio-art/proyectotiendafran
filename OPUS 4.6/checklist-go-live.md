# Checklist Go-Live - Fase 1
## Criterios de Lanzamiento: Tienda Fran

**Fecha:** 2026-02-09
**Responsable de validacion:** [Nombre del responsable]
**Audiencia:** equipo de desarrollo

---

## Instrucciones

Cada criterio debe ser validado y marcado antes de la salida a produccion.

- **OK** = cumplido y verificado
- **PARCIAL** = funciona pero con limitaciones aceptadas
- **FALLA** = no cumplido, blocker de lanzamiento

Si algun criterio critico (marcado con **BLOCKER**) esta en FALLA, no se lanza. Se recomienda salida controlada (beta con grupo reducido).

---

## 1. Flujo del Cliente (B2C)

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 1.1 | Un cliente puede navegar el catalogo completo por categorias | BLOCKER | [ ] | | |
| 1.2 | Un cliente puede ver el detalle de un producto con precio e imagen | BLOCKER | [ ] | | |
| 1.3 | Un cliente puede agregar productos al carrito | BLOCKER | [ ] | | |
| 1.4 | El carrito persiste al cerrar y reabrir el navegador | Importante | [ ] | | |
| 1.5 | Un cliente puede completar el checkout con retiro en local | BLOCKER | [ ] | | |
| 1.6 | Un cliente puede completar el checkout con envio a domicilio | BLOCKER | [ ] | | |
| 1.7 | El cliente recibe confirmacion con ID de pedido y resumen | BLOCKER | [ ] | | |
| 1.8 | El cliente puede consultar el estado de su pedido con el ID | Importante | [ ] | | |
| 1.9 | Si el local esta cerrado, se muestra mensaje y se bloquea el checkout | BLOCKER | [ ] | | |
| 1.10 | Si un producto fue pausado, no aparece en el catalogo | BLOCKER | [ ] | | |
| 1.11 | El costo de envio se muestra correctamente en el carrito y checkout | BLOCKER | [ ] | | |
| 1.12 | Si hay pedido minimo para envio, se bloquea correctamente | Importante | [ ] | | |

---

## 2. Flujo del Admin

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 2.1 | Admin puede loguearse al panel con credenciales validas | BLOCKER | [ ] | | |
| 2.2 | Credenciales invalidas no permiten acceso (error generico) | BLOCKER | [ ] | | |
| 2.3 | Admin ve pedidos nuevos en la bandeja | BLOCKER | [ ] | | |
| 2.4 | Admin puede cambiar estado de pedido: Nuevo -> En prep -> Listo -> Enviado/Retirado -> Cerrado | BLOCKER | [ ] | | |
| 2.5 | Admin puede cancelar un pedido con motivo registrado | BLOCKER | [ ] | | |
| 2.6 | El historial de cambios de estado se registra con timestamps | BLOCKER | [ ] | | |
| 2.7 | Admin recibe alerta (sonido/visual) cuando entra un pedido nuevo | Importante | [ ] | | |
| 2.8 | Admin puede crear un producto nuevo con imagen | BLOCKER | [ ] | | |
| 2.9 | Admin puede editar precio/nombre de un producto existente | BLOCKER | [ ] | | |
| 2.10 | Admin puede pausar/despausar un producto | BLOCKER | [ ] | | |
| 2.11 | Admin puede crear/editar categorias | BLOCKER | [ ] | | |

---

## 3. Configuracion del Local

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 3.1 | Admin puede configurar horarios de apertura/cierre por dia | BLOCKER | [ ] | | |
| 3.2 | Los horarios impactan correctamente: fuera de horario = tienda cerrada | BLOCKER | [ ] | | |
| 3.3 | Admin puede activar/desactivar pausa manual | BLOCKER | [ ] | | |
| 3.4 | La pausa cierra la tienda independientemente del horario | BLOCKER | [ ] | | |
| 3.5 | Admin puede configurar opciones de entrega (retiro/envio) | BLOCKER | [ ] | | |
| 3.6 | Admin puede configurar costo de envio (fijo o por zona) | BLOCKER | [ ] | | |

---

## 4. Seguridad y Validaciones

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 4.1 | Backend recalcula y valida totales al crear pedido (no confia en el cliente) | BLOCKER | [ ] | | |
| 4.2 | No se pueden crear pedidos con productos pausados | BLOCKER | [ ] | | |
| 4.3 | No se pueden crear pedidos con local cerrado/pausado | BLOCKER | [ ] | | |
| 4.4 | Se guardan snapshots de precios en order_items | BLOCKER | [ ] | | |
| 4.5 | Panel admin inaccesible sin autenticacion (redirect a login) | BLOCKER | [ ] | | |
| 4.6 | Rate limiting en endpoint de login | Importante | [ ] | | |
| 4.7 | Transiciones de estado invalidas son rechazadas por el backend | BLOCKER | [ ] | | |
| 4.8 | Validaciones server-side en todos los formularios (no solo client-side) | BLOCKER | [ ] | | |

---

## 5. Testing en Dispositivos

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 5.1 | Flujo completo probado en celular real (Android) | BLOCKER | [ ] | | |
| 5.2 | Flujo completo probado en celular real (iOS/Safari) | BLOCKER | [ ] | | |
| 5.3 | Panel admin probado en desktop (Chrome) | BLOCKER | [ ] | | |
| 5.4 | Panel admin probado en tablet | Importante | [ ] | | |
| 5.5 | Catalogo carga en tiempo razonable en 4G | Importante | [ ] | | |

---

## 6. Infraestructura y Produccion

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 6.1 | Aplicacion desplegada con dominio propio y SSL (HTTPS) | BLOCKER | [ ] | | |
| 6.2 | Base de datos productiva funcionando | BLOCKER | [ ] | | |
| 6.3 | Backup diario de base de datos configurado | BLOCKER | [ ] | | |
| 6.4 | Restauracion de backup probada al menos una vez | BLOCKER | [ ] | | |
| 6.5 | Monitoreo de errores activo (Sentry o similar) | Importante | [ ] | | |
| 6.6 | Monitoreo de uptime activo (alerta si el sitio se cae) | Importante | [ ] | | |
| 6.7 | Variables de entorno de produccion configuradas (no hardcodeadas) | BLOCKER | [ ] | | |
| 6.8 | Deploy automatico configurado (push a main = deploy) | Importante | [ ] | | |

---

## 7. Operacion y Capacitacion

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 7.1 | Capacitacion al personal del local realizada | BLOCKER | [ ] | | |
| 7.2 | Personal practico flujo completo en vivo (al menos 1 pedido real de prueba) | BLOCKER | [ ] | | |
| 7.3 | Guia breve de uso entregada | Importante | [ ] | | |
| 7.4 | Datos iniciales cargados: categorias y productos del local | BLOCKER | [ ] | | |
| 7.5 | Horarios del local configurados | BLOCKER | [ ] | | |
| 7.6 | Opciones de envio y costos configurados | BLOCKER | [ ] | | |
| 7.7 | Canal de soporte definido (WhatsApp/email para reportar problemas) | BLOCKER | [ ] | | |

---

## 8. Plan de Lanzamiento

| # | Criterio | Tipo | Estado | Verificado por | Fecha |
|---|---|---|---|---|---|
| 8.1 | QR generado para poner en el local (apunta a la tienda) | Importante | [ ] | | |
| 8.2 | Mensaje de difusion preparado para mandar a clientes actuales | Importante | [ ] | | |
| 8.3 | Plan de rollback definido (que hacer si hay un problema critico) | BLOCKER | [ ] | | |
| 8.4 | Horario de lanzamiento acordado (preferible dia tranquilo, no finde) | Importante | [ ] | | |

---

## Resumen de Decision

| Criterio | Resultado |
|---|---|
| **Total BLOCKER** | ___ de ___ cumplidos |
| **Total Importante** | ___ de ___ cumplidos |

### Decision final

- [ ] **GO:** todos los BLOCKER cumplidos, lanzamiento pleno
- [ ] **GO PARCIAL:** todos los BLOCKER cumplidos, algunos Importantes pendientes, salida controlada (beta)
- [ ] **NO-GO:** hay BLOCKERS sin cumplir, se reprograma

**Fecha de lanzamiento acordada:** _______________
**Firmado por:** _______________

---

*Checklist basado en los criterios definidos en el documento consolidado del proyecto. Se completa durante la semana previa al lanzamiento.*
