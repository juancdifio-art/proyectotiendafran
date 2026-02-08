# Propuesta consolidada para presentar (martes)
## Sistema de pedidos y gestion comercial - enfoque por fases

**Cliente:** [Nombre del cliente]  
**Fecha:** [Completar]  
**Preparado por:** [Tu equipo]

---

## 1. Resumen ejecutivo
Proponemos una implementacion incremental para digitalizar el negocio sin frenar la operacion diaria:

- Fase 0: Discovery y definicion cerrada del MVP
- Fase 1: Tienda online del local (`single-store`) + panel de pedidos
- Fase 1.5: Mejoras operativas (pagos online, reportes, comanda)
- Fase 2: Canal mayorista (B2B) con reglas propias
- Fase 3 (vision): evolucion a plataforma multi-comercio en Necochea

La clave es salir rapido con una primera version util y escalar con datos reales.

---

## 2. Problema de negocio que resolvemos
- Pedidos por canales dispersos (WhatsApp, mostrador, llamadas).
- Poco control operativo de pedidos en tiempo real.
- Riesgo de errores por procesos manuales.
- Oportunidad de vender mas sin comisiones altas de terceros.

---

## 3. Alcance por fases

## Fase 0 - Discovery (1-2 semanas)
**Objetivo:** cerrar alcance real, riesgos y costos finales.

**Incluye:**
- Relevamiento funcional y operativo.
- Definicion de reglas criticas: delivery, horarios, minimos, estados, datos del cliente.
- Prototipo rapido de flujo (catalogo -> carrito -> checkout -> panel admin).
- Backlog priorizado y plan tecnico.

**Entregables:**
- Documento de alcance MVP firmado.
- Roadmap por fases.
- Presupuesto final por etapa.

## Fase 1 - MVP `single-store` (6-8 semanas)
**Objetivo:** vender online desde el local con una operacion estable.

**Cliente (B2C):**
- Catalogo por categorias.
- Carrito + checkout.
- Retiro en local y envio local.
- Confirmacion de pedido con ID.

**Admin local:**
- Login admin.
- Bandeja de pedidos con estados: `Nuevo -> En preparacion -> Listo -> Entregado/Retirado -> Cerrado/Cancelado`.
- CRUD de productos/categorias.
- Horarios y pausa de pedidos.

**Fuera de alcance en Fase 1:**
- Marketplace multi-comercio.
- Tracking de repartidor en mapa.
- Integraciones AFIP/contables.
- Integracion profunda con sistema legacy (DataLife), salvo API clara y prioridad acordada.

## Fase 1.5 - Optimizacion operativa (2-4 semanas)
- Integracion MercadoPago.
- Comanda/impresion operativa.
- Reportes base (ventas por dia/producto, ticket promedio).
- Ajustes UX y performance segun uso real.

## Fase 2 - Canal mayorista B2B (4-6 semanas)
- Login cerrado para clientes mayoristas.
- Listas de precio por cliente/rubro.
- Minimos de compra y condiciones.
- Historial y repeticion de pedidos.
- Entrega programada.
- Base para cuenta corriente (si se contrata modulo adicional).

## Fase 3 - Vision marketplace (a evaluar)
- Multi-store.
- Onboarding comercios.
- Comisiones y liquidaciones.
- Soporte y reclamos centralizados.

---

## 4. Propuesta tecnica recomendada
- Frontend/App web: `Next.js` (mobile-first, PWA opcional).
- Backend/API: `Next.js API` o `Node.js` segun arquitectura final del equipo.
- Base de datos: `PostgreSQL`.
- ORM: `Prisma`.
- Auth: roles `customer`, `store_admin`, `platform_admin` (futuro).
- Infra: cloud + backups + monitoreo.

Nota: mantener el stack alineado al equipo reduce tiempos, costo y riesgo.

---

## 5. Propuesta economica (rango de referencia)
Se recomienda cotizar en USD o en ARS al tipo de cambio acordado al momento de firma.

## Opcion A - Entrada controlada (recomendada para cerrar rapido)
- Fase 0 + Fase 1
- Rango: **USD 6,000 - 10,000**

## Opcion B - Operacion consolidada
- Fase 0 + Fase 1 + Fase 1.5
- Rango: **USD 10,000 - 16,000**

## Opcion C - Expansion mayorista
- Fase 0 + Fase 1 + Fase 1.5 + Fase 2
- Rango: **USD 16,000 - 26,000**

## Costos mensuales estimados
- Infraestructura (hosting/backups/monitoreo): **USD 30 - 120 / mes**
- Soporte y mantenimiento: **USD 120 - 350 / mes**

---

## 6. Condiciones comerciales sugeridas
- Modalidad: por hitos.
- Anticipo: 30% al inicio.
- Esquema sugerido: 30% inicio + 30% aprobacion UX/flujo + 30% entrega funcional + 10% salida productiva.
- Garantia: 30 dias de correcciones post salida (sin nuevas funcionalidades).
- Cambios de alcance: se cotizan como adicionales.

---

## 7. Riesgos y mitigacion
- Riesgo: alcance demasiado grande desde el dia 1.
  - Mitigacion: contrato por fases, con corte formal al final de cada etapa.
- Riesgo: reglas de stock mal definidas.
  - Mitigacion: taller operativo obligatorio en Discovery.
- Riesgo: agregar integraciones fiscales/contables a mitad de proyecto.
  - Mitigacion: explicitar como modulo aparte antes de iniciar desarrollo.

---

## 8. Guion corto para presentar al cliente
1. "No te vamos a vender humo de marketplace desde el dia 1."
2. "Primero te ponemos a vender online con operacion ordenada."
3. "Con esa base estable, sumamos mayorista y automatizaciones."
4. "Cada fase tiene alcance cerrado, costo claro y entregables concretos."

---

## 9. Proximos pasos inmediatos
1. Validar esta propuesta internamente (ustedes dos).
2. Completar datos comerciales (nombre, moneda, condiciones exactas).
3. Preparar version PDF con branding para enviar/presentar el martes.
