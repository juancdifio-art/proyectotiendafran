# Anteproyecto y Propuesta Económica
## Sistema de Gestión Integral y Plataformas de Pedidos

---

**Fecha:** [Fecha de hoy]
**Para:** [Nombre del Cliente / Nombre del Negocio]
**De:** [Nombre de tu Empresa/Estudio]
**Contacto:** [Teléfono] | [Email] | [Web]

---

## 1. Resumen Ejecutivo

Se propone implementar una **solución integral** para modernizar y centralizar la operación de un local comercial híbrido que combina venta minorista directa al público con distribución mayorista (B2B) a comercios de la zona.

**La solución incluye:**
- **Sistema de Gestión Central** (Backend + Panel Admin Web) para control de stock, ventas y operaciones
- **App Minorista (B2C)** - tipo "PedidosYa" exclusiva del local para clientes finales
- **App Mayorista (B2B)** - para pedidos de comercios registrados

Los tres componentes se conectan a una única base de datos, garantizando **stock unificado en tiempo real** y eliminando duplicación de tareas.

---

## 2. Comprensión del Negocio

### El Desafío
El cliente opera un modelo de negocio híbrido:
- **Venta minorista:** Comidas rápidas, kiosco, sándwiches, helados (atención al público)
- **Venta mayorista:** Distribución al por mayor a otros comercios de la zona

**Problemas actuales:**
- Stock del local y pedidos de apps gestionados por separado
- Pedidos mayoristas vía WhatsApp (errores, tiempo perdido)
- Sin visibilidad en tiempo real de ventas y stock
- Dependencia de plataformas como PedidosYa (comisiones del 20-30%)

### El Valor Diferencial de Esta Solución

1. **"La Verdad Única del Stock":** Si vende el último helado en el local, se pausa automáticamente en la App Minorista. Un solo inventario para todos los canales.

2. **Eficiencia Mayorista:** La App B2B elimina horas de tomar pedidos por WhatsApp, evita errores de anotación y permite que los comercios compren 24/7.

3. **Propiedad de los Datos:** A diferencia de PedidosYa, el cliente es dueño de su base de datos, no paga comisiones por venta y puede hacer marketing directo (notificaciones push) a sus clientes.

---

## 3. Alcance Funcional

### 3.1 Módulo Central (Backend + Admin Web)

| Módulo | Funcionalidades |
|--------|-----------------|
| **Productos** | Categorías (kiosco, helados, sándwiches, bebidas), variantes (tamaños/sabores), imágenes, descripciones, precios minorista y mayorista |
| **Stock** | Control en tiempo real, alertas de bajo stock, movimientos (venta, ajuste, merma, ingreso, devolución), historial/auditoría |
| **Pedidos** | Estados (pendiente, confirmado, en preparación, listo, entregado, cancelado), observaciones, asignación a cocina |
| **Clientes** | Minoristas (registro automático), Mayoristas (CUIT, listas de precio, condiciones, límite de crédito, estado de cuenta) |
| **Precios** | Precio minorista (PVP), precio mayorista (por lista o por cliente) |
| **Reportes** | Ventas por día/semana/mes, por producto, por canal, productos más vendidos, stock bajo/faltantes |
| **Usuarios** | Roles: Administrador, Operador, Vendedor mayorista (opcional) |
| **Auditoría** | Logs de movimientos críticos (stock, precios, cancelaciones) |

### 3.2 App Minorista (B2C) - "Tipo PedidosYa del Local"

**MVP (Versión Inicial):**
| Funcionalidad | Detalle |
|---------------|---------|
| Registro/Login | Con email, teléfono (SMS) o como invitado |
| Catálogo | Menú visual con fotos, categorías, búsqueda |
| Carrito | Agregar/modificar productos, notas ("sin mayo", "extra queso") |
| Entrega | Retiro en local o delivery (radio configurable) |
| Horarios | Disponibilidad según horarios de atención |
| Notificaciones | Push en tiempo real del estado del pedido |
| Pagos | Efectivo, MercadoPago, transferencia |

**Evolutivo (Fases Posteriores):**
- Promociones / cupones de descuento
- Programa de fidelidad
- Seguimiento del repartidor en mapa
- Zonas de entrega con costo por distancia
- Integración WhatsApp para notificaciones

### 3.3 App Mayorista (B2B) - "Pedidos de Comercios"

**MVP (Versión Inicial):**
| Funcionalidad | Detalle |
|---------------|---------|
| Login cerrado | Solo clientes aprobados por el administrador |
| Catálogo B2B | Precios mayoristas, presentaciones por bulto/caja |
| Condiciones | Mínimo de compra, días de entrega, cortes de pedido |
| Historial | Consulta de pedidos anteriores |
| Repetir pedido | "Volver a comprar" con un clic |
| Entrega programada | Selección de fecha/horario de entrega |
| Notificaciones | Confirmación cuando el pedido está aprobado |

**Evolutivo (Fases Posteriores):**
- Cuenta corriente / gestión de crédito
- Consulta de saldo y estado de deuda
- Facturación electrónica (integración AFIP)
- Descarga de remitos/facturas en PDF
- Ruteo de reparto (optimización de recorridos)

### 3.4 Alcance NO Incluido (Exclusiones)

Para evitar malentendidos, esto NO está incluido salvo módulo adicional:
- Integración con AFIP / facturación electrónica
- Integración con impresoras fiscales / hardware POS específico
- Sistema contable completo (asientos, balances)
- Marketplace multi-local (varios comercios)
- Integración con sistemas ERP externos

---

## 4. Propuesta Técnica

| Componente | Tecnología Sugerida | Justificación |
|------------|---------------------|---------------|
| **Apps Móviles** | Flutter | Cross-platform (iOS + Android con un solo código), alto rendimiento |
| **Admin Web** | React / Vue.js | Framework moderno, escalable, fácil mantenimiento |
| **Backend** | Node.js o Laravel (PHP) | Según stack del equipo, robusto y escalable |
| **Base de Datos** | PostgreSQL o MySQL | Relacional, confiable, con respaldo |
| **Pasarela de Pagos** | MercadoPago | Ampliamente aceptada, fácil integración |
| **Notificaciones** | Firebase Cloud Messaging | Push en tiempo real |
| **Hosting** | Cloud (AWS / Google Cloud / DigitalOcean) | Seguridad, backups automáticos, alta disponibilidad |
| **Autenticación** | JWT + roles | Seguro, estándar de la industria |

---

## 5. Cronograma por Fases

| Fase | Duración | Actividades Clave | Entregables |
|------|----------|-------------------|-------------|
| **0. Inicio / Discovery** | 1-2 sem | Relevamiento final, definición MVP, cierre de reglas (stock, variantes, precios, zonas) | Documento de requerimientos |
| **1. Diseño UX/UI** | 2-3 sem | Prototipo app minorista + mayorista + admin, aprobación del cliente | Mockups navegables |
| **2. Desarrollo Núcleo** | 4-5 sem | Backend + base de datos + admin web (productos, clientes, stock, pedidos) | Panel Admin funcional |
| **3. Desarrollo Apps** | 4-5 sem | App Minorista (3 sem) + App Mayorista (2 sem) | Apps para testing |
| **4. QA + Integración** | 2 sem | Testing integral, pruebas de estrés, correcciones | Sistema estable |
| **5. Salida + Capacitación** | 1 sem | Deploy, publicación en stores, entrenamiento al personal, carga de datos | Sistema en producción |

**Duración Total Estimada: 14-18 semanas**

---

## 6. Presupuesto

### 6.1 Opciones de Desarrollo

| Opción | Incluye | USD | ARS (ref.)* |
|--------|---------|-----|-------------|
| **A. MVP Operativo** | Admin + stock + ventas + pedidos minorista + pedidos mayorista. Sin pagos online ni ruteo avanzado. | $8,000 - $15,000 | $8.000.000 - $15.000.000 |
| **B. Estándar (Recomendado)** | MVP + promociones básicas, zonas de entrega, notificaciones robustas, reportes mejorados, perfiles/roles completos. | $15,000 - $25,000 | $15.000.000 - $25.000.000 |
| **C. Premium** | Estándar + pagos online integrados, ruteo/gestión de reparto, cuenta corriente mayorista, integraciones contables. | $25,000 - $40,000 | $25.000.000 - $40.000.000 |

*Tipo de cambio referencial: 1 USD = 1.000 ARS. Ajustar al momento de firma.

### 6.2 Desglose por Módulo (Opción B - Estándar)

| Módulo | Descripción | USD | ARS (ref.) |
|--------|-------------|-----|------------|
| Diseño UX/UI | Diseño de todas las pantallas (admin + 2 apps) | $2,000 - $3,500 | $2.000.000 - $3.500.000 |
| Sistema Central | Backend + Panel Web + Base de datos | $5,000 - $8,000 | $5.000.000 - $8.000.000 |
| App Minorista (B2C) | Desarrollo iOS + Android | $3,500 - $5,500 | $3.500.000 - $5.500.000 |
| App Mayorista (B2B) | Desarrollo iOS + Android | $2,500 - $4,500 | $2.500.000 - $4.500.000 |
| Pasarela de Pagos | Integración MercadoPago | $1,000 - $1,500 | $1.000.000 - $1.500.000 |
| Capacitación + Deploy | Carga de datos, entrenamiento, publicación | $1,000 - $2,000 | $1.000.000 - $2.000.000 |
| **TOTAL** | | **$15,000 - $25,000** | **$15.000.000 - $25.000.000** |

### 6.3 Costos Recurrentes (Mensuales)

| Concepto | USD/mes | ARS/mes (ref.) |
|----------|---------|----------------|
| Servidor + backups + monitoreo | $30 - $100 | $30.000 - $100.000 |
| Servicios (notificaciones, email, SMS) | $10 - $30 | $10.000 - $30.000 |
| Mantenimiento y soporte técnico | $100 - $250 | $100.000 - $250.000 |
| **TOTAL MENSUAL** | **$140 - $380** | **$140.000 - $380.000** |

---

## 7. Condiciones Comerciales

| Concepto | Detalle |
|----------|---------|
| **Modalidad** | Por hitos (fases) con entregas parciales |
| **Anticipo** | 30% al inicio del proyecto |
| **Pagos por hito** | 30% al aprobar UX/UI + 30% al entregar MVP + 10% al salir a producción |
| **Garantía** | 30 días de correcciones post salida (no incluye nuevas funcionalidades) |
| **Soporte** | Bolsa mensual de horas o plan de mantenimiento a acordar |

---

## 8. Riesgos y Supuestos

### Supuestos
- Un solo local (una operación central)
- Stock por producto (y variantes si hace falta), no por múltiples depósitos
- Mayorista con login cerrado y listas de precio por cliente
- Sin integración fiscal/AFIP en el MVP

### Riesgos y Mitigación

| Riesgo | Impacto | Mitigación |
|--------|---------|------------|
| Regla de stock mal definida (mostrador vs apps vs mermas) | Descuadres de inventario | Taller de procesos en Fase 0 |
| Cambios de alcance durante desarrollo | Atrasos y sobrecostos | Firmar alcance MVP antes de iniciar |
| Solicitud de facturación electrónica/AFIP | Impacto fuerte en tiempos | Definir en Discovery si es requerido |

---

## 9. Próximos Pasos

### Opción Recomendada: Iniciar con Discovery

Antes de comprometer el desarrollo completo, proponemos una **fase de Discovery** paga (descontable del total):

| Fase Discovery | Detalle |
|----------------|---------|
| **Duración** | 1-2 semanas |
| **Incluye** | Relevamiento detallado, definición del MVP, prototipo de pantallas principales, backlog priorizado, cronograma y presupuesto final cerrado |
| **Costo** | $500 - $1,500 USD (descontable si se contrata el proyecto completo) |

### Pasos Formales

1. **Revisión** - El cliente revisa esta propuesta
2. **Reunión de consulta** - Aclarar dudas y ajustar detalles
3. **Aprobación formal** - Firma de acuerdo y pago de anticipo
4. **Kick-off** - Inicio formal del proyecto

---

## 10. Anexo: Checklist de Funcionalidades

### Incluido en MVP
- [ ] Productos / categorías / variantes
- [ ] Stock + movimientos (venta, ajuste, merma, ingreso)
- [ ] Pedidos minorista (retiro/envío, horarios, notas)
- [ ] Pedidos mayorista (mínimos, listas, repetición)
- [ ] Clientes mayoristas (condiciones, listas)
- [ ] Reportes básicos
- [ ] Notificaciones push
- [ ] Roles y permisos
- [ ] Deploy + backups
- [ ] Capacitación

### Evolutivo (fases posteriores)
- [ ] Promociones / cupones
- [ ] Programa de fidelidad
- [ ] Cuenta corriente mayorista
- [ ] Facturación electrónica / AFIP
- [ ] Ruteo de reparto
- [ ] BI / reportes avanzados

---

**Estamos convencidos de que esta solución no solo resolverá las necesidades operativas actuales, sino que potenciará el crecimiento del negocio, posicionándolo como un comercio moderno y eficiente.**

Quedamos a su completa disposición para cualquier consulta.

---

**[Tu Empresa de Desarrollo]**
[Teléfono] | [Email] | [Web]

---

*Firma del Cliente al aprobar: _________________ Fecha: ___/___/______*
