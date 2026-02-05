Anteproyecto: Sistema de Gestión Integral para Local Comercial
(Control de Stock, Ventas + Apps de Pedidos Minorista/Mayorista)

1. Introducción
El cliente opera un local comercial con doble enfoque:
✅ Venta minorista: Comidas rápidas, kiosko, sándwiches, helados (atención al público).
✅ Venta mayorista: Suministro al por mayor a otros comercios de la zona.

Necesidades clave:

Control centralizado de ventas y stock (evitar faltantes/sobrestock).
App para clientes minoristas (similar a PedidosYa, exclusiva para su local).
App para clientes mayoristas (pedidos al por mayor).
Este anteproyecto detalla alcance, tecnologías, cronograma y presupuesto estimado para su aprobación.

2. Alcance del Proyecto
A. Módulo Central de Gestión (Backoffice - Web)
(Accesible desde cualquier dispositivo con navegador - para el dueño/empleados)

Gestión de Inventario (Stock)

Registro de todos los productos (código, nombre, categoría, precio minorista, precio mayorista, costo, stock actual).
Alertas automáticas de bajo stock (configurable por producto).
Movimientos de stock: entradas (compras a proveedores), salidas (ventas minoristas/mayoristas), ajustes.
Historial de movimientos.
Gestión de Ventas

Registro de ventas en local (vía tablet o PC en el mostrador).
Registro automático de ventas generadas desde las apps móviles.
Emisión de facturas/remitos (opcional: integración con AFIP si el cliente lo requiere).
Informes detallados:
Ventas diarias/semanales/mensuales.
Ventas por producto, por cliente (mayorista/minorista).
Productos más vendidos.
Rentabilidad por producto.
Gestión de Clientes

Clientes Minoristas: Registro automático al hacer su primer pedido por la app (nombre, teléfono, dirección de entrega).
Clientes Mayoristas:
Alta manual con datos completos (Razón Social, CUIT, contacto, dirección, límite de crédito asignado, precios especiales).
Historial de compras al por mayor.
Estado de cuenta (saldo adeudado).
Compras a Proveedores

Registro de proveedores.
Órdenes de compra.
Control de costos vs. precios de venta.
Usuarios y Roles

Administrador (acceso total).
Empleado de ventas (solo ventas, stock y pedidos).
Dueño (informes financieros).
B. App Móvil para Clientes MINORISTAS
(Descargable desde App Store y Google Play - Exclusiva para este local)

Funcionalidad	Detalle
Registro/Login	Con número de teléfono (código SMS) o email.
Menú interactivo	Categorías: Comidas rápidas, Sándwiches, Helados, Kiosko, etc. Con imágenes, descripción y precios.
Carrito de compras	Agregar, modificar o eliminar productos.
Opciones de entrega/retiro	- Retiro en local <br> - Delivery (solo dentro de un radio predefinido, ej: 5 km).
Medios de pago	- Efectivo al retirar <br> - Tarjeta de crédito/débito (vía pasarela segura: MercadoPago o TodoPago) <br> - Transferencia bancaria (opcional)
Seguimiento del pedido	Notificaciones en tiempo real: “Recibido”, “En preparación”, “En camino”, “Entregado”.
Historial de pedidos	Consulta de pedidos anteriores.
Promociones y descuentos	Cupones exclusivos para usuarios frecuentes.
⚠️ Nota: La app será branded con logo, colores y nombre del local (ej: “Comidas Rápidas [NombreLocal] - Pedidos”).

C. App Móvil para Clientes MAYORISTAS
(Solo para comercios registrados - Descargable o acceso web responsive)

Funcionalidad	Detalle
Login con credenciales	Usuario y contraseña asignados por el local (solo comercios autorizados).
Catálogo con precios MAYORISTAS	Precios diferenciados (no visibles para minoristas).
Pedido al por mayor	Capacidad para pedir grandes cantidades (ej: 50 sándwiches, 20 litros de helado).
Carga de datos para facturación	El cliente mayorista ingresa sus datos fiscales (CUIT, dirección) para que el remito/factura se genere automáticamente.
Seguimiento de pedidos	Estado del pedido y fecha estimada de entrega.
Historial y estado de cuenta	Consulta de todas las compras realizadas y saldo pendiente (si hay crédito).
Descarga de remitos/facturas	En formato PDF.
💡 Opción adicional (recomendada): La app mayorista puede ser una versión web responsive (accesible desde cualquier navegador), evitando el desarrollo de dos apps móviles separadas y reduciendo costos.

3. Tecnologías Propuestas
Componente	Tecnología	Razón
Backoffice (Web)	Laravel (PHP) + MySQL	Framework robusto, seguro, ideal para sistemas de gestión. Escalable.
Apps Móviles	Flutter (desarrollo cross-platform → 1 código para iOS y Android)	Reduce costos y tiempo. Alto rendimiento.
Pasarela de Pagos	MercadoPago o TodoPago	Ampliamente aceptadas en Argentina, fácil integración.
Servidor/Hosting	Cloud (AWS, Google Cloud o Hostinger)	Seguridad, respaldo automático y alta disponibilidad.
Notificaciones Push	Firebase Cloud Messaging (FCM)	Envío de notificaciones en tiempo real a las apps.
4. Cronograma Estimado (Aprox. 12-14 semanas)
Fase	Duración	Actividades clave
1. Análisis y Diseño	2 semanas	Reuniones de detalle, diagramas de flujo, diseño de interfaz (UI/UX), definición de BD.
2. Desarrollo Backoffice	4 semanas	Módulos de stock, ventas, clientes, informes.
3. Desarrollo Apps Móviles	5 semanas	- App Minorista (3 sem)<br>- App Mayorista (2 sem) (o versión web)
4. Integración y Pruebas	2 semanas	Conexión apps ↔ backoffice, pruebas de estrés, pruebas de usabilidad con usuarios reales.
5. Capacitación & Carga Inicial	1 semana	Entrenamiento al cliente, carga de productos, clientes mayoristas y proveedores.
6. Lanzamiento	1 semana	Publicación en stores (si aplica), puesta en producción.
Tiempo Total Estimado: 15 semanas (3.5 meses)

5. PRESUPUESTO ESTIMADO
(Valores en ARS - Actualizado a Octubre 2023)

Módulo	Costo	Detalle
Desarrollo del Backoffice (Web)	$850.000	Módulos de stock, ventas, clientes, informes, usuarios.
App Minorista (Flutter - iOS + Android)	$600.000	Diseño, desarrollo, pruebas, publicación en stores.
App/Sistema Mayorista	$450.000	Opción A (App móvil): $450.000<br>Opción B (Web responsive): $300.000 (recomendada)
Integración Pasarela de Pagos	$150.000	Configuración con MercadoPago/TodoPago.
Configuración Inicial & Capacitación	$100.000	Carga de datos iniciales (productos, clientes), entrenamiento al personal.
Hosting & Mantenimiento (1 año)	$120.000	(Opcional pero recomendado)<br>Incluye: hosting, actualizaciones, soporte técnico básico.
TOTAL ESTIMADO	$2.270.000	(Con App Mayorista como Web Responsive → $2.120.000)
Notas sobre el presupuesto:
🔹 Los precios incluyen IVA.
🔹 No incluye costos adicionales por:

Desarrollo de funcionalidades no especificadas en este anteproyecto.
Integración con sistemas contables externos (ej: SAP, ContaPlus).
🔹 Garantía: 3 meses de soporte técnico post-entrega para corrección de errores.
💡 Recomendación para reducir costos:
Implementar la solución mayorista como aplicación web responsive (accesible desde cualquier navegador) en lugar de una app móvil nativa. Esto ahorra ~$150.000.

6. Próximos Pasos
Aprobación del anteproyecto y presupuesto por parte del cliente.
Firma del contrato formal (incluye detalles técnicos, plazos y condiciones de pago).
Pago inicial (30%) para dar inicio al proyecto.
Reuniones semanales de seguimiento.
📅 Tiempo máximo para aprobación: 5 días hábiles.
¡Comencemos a digitalizar su negocio!

Elaborado por:
[Tu Empresa de Desarrollo de Software]
Contacto: [Teléfono] | [Email] | [Web]

Firma y sello del cliente al aprobar el anteproyecto.

Firma del Cliente
Fecha: //_______