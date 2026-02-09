# Guia de Reunion entre Socios
## Anteproyecto y Presupuesto (base: `proyecto-consolidado-final.md`)

**Objetivo:** salir de la reunion con decisiones cerradas para armar propuesta comercial y presupuesto.

---

## 1) Preparacion previa (15-20 min cada uno)
- Leer completo `proyecto-consolidado-final.md`.
- Marcar en notas personales:
  - que se mantiene sin cambios
  - que se ajusta
  - que todavia no convence
- Llevar un numero objetivo de cierre comercial:
  - precio minimo aceptable
  - precio recomendado
  - precio ideal

---

## 2) Resultado obligatorio de la reunion
Al terminar, deben existir estos 5 outputs:

1. Alcance final Fase 1 (incluye y excluye).
2. Decision de arquitectura (Opcion A u Opcion B).
3. Modelo de propiedad/licencia acordado para este cliente.
4. Presupuesto en 2 o 3 escenarios.
5. Proximo paso comercial concreto (que se envia y cuando).

Si falta uno de estos 5, la reunion queda incompleta.

---

## 3) Duracion sugerida y agenda (90 min)
## Bloque 1 - Alineacion inicial (10 min)
- Confirmar objetivo de la reunion.
- Confirmar restriccion comercial: cliente probablemente no pague ticket alto de entrada.

## Bloque 2 - Alcance Fase 1 (20 min)
- Cerrar lista de "SI incluye".
- Cerrar lista de "NO incluye".
- Definir el corte exacto entre F1 y F1.5.

## Bloque 3 - Arquitectura (15 min)
- Resolver Opcion A (Astro + API separada) vs Opcion B (Next fullstack).
- Criterio principal para decidir: velocidad de salida y riesgo operativo.

## Bloque 4 - Propiedad y licenciamiento (15 min)
- Acordar que es del cliente y que es del equipo.
- Acordar como se plantea al cliente y en que etapa (Discovery/propuesta/contrato).

## Bloque 5 - Presupuesto y modelo de cobro (20 min)
- Definir Discovery.
- Definir F1.
- Definir esquema de pagos por hitos.
- Definir abono mensual de soporte.

## Bloque 6 - Cierre ejecutivo (10 min)
- Lista final de acuerdos.
- Lista de pendientes con responsable y fecha.
- Definir documento y mensaje para el cliente.

---

## 4) Reglas de la reunion (para que no se trabe)
- Una sola persona facilita y cuida el tiempo.
- Toda decision queda escrita en el momento.
- Si un tema supera 10 min sin acuerdo:
  - se registra como pendiente
  - se define responsable
  - se sigue con el siguiente punto
- No discutir implementacion tecnica fina en esta reunion, solo decisiones de anteproyecto y comercial.

---

## 5) Checklist de decisiones (usar en vivo)
## A) Alcance Fase 1
- [ ] Flujo pedido completo cliente -> admin -> cierre
- [ ] CRUD productos/categorias
- [ ] Horarios + pausa de pedidos
- [ ] Delivery simple (fijo o zona)
- [ ] Sin AFIP, sin marketplace, sin tracking

## B) Arquitectura
- [ ] Opcion elegida: A o B
- [ ] Justificacion en 1 parrafo
- [ ] Riesgo principal de la opcion elegida
- [ ] Mitigacion de ese riesgo

## C) Propiedad/licenciamiento
- [ ] Datos del cliente: titularidad del cliente
- [ ] Core reutilizable: titularidad del equipo
- [ ] Licencia de uso del sistema para el cliente
- [ ] Condicion de escalado a marketplace
- [ ] Beneficio fundador (si aplica)

## D) Presupuesto
- [ ] Escenario minimo (entrada)
- [ ] Escenario recomendado
- [ ] Escenario expansion
- [ ] Abono mensual
- [ ] Hitos de pago

---

## 6) Plantilla de acta de acuerdos (copiar y completar)

### Acuerdos cerrados
1. Alcance F1:
2. Arquitectura:
3. Modelo de propiedad/licencia:
4. Presupuesto:
5. Modelo de cobro:

### Pendientes
1. Tema:
   Responsable:
   Fecha limite:
2. Tema:
   Responsable:
   Fecha limite:

### Decisiones para cliente
1. Documento a enviar:
2. Fecha de envio:
3. Mensaje de presentacion:

---

## 7) Propuesta de escenarios de precio para discutir
## Escenario 1 - Entrada (cerrar rapido)
- Discovery + F1 recortada
- Precio bajo de entrada
- Mantenimiento mensual obligatorio

## Escenario 2 - Recomendado
- Discovery + F1 completa + F1.5 parcial
- Mejor equilibrio entre resultado y margen

## Escenario 3 - Expansion
- Incluye base B2B
- Se activa solo si el cliente valida F1

Nota: si el cliente solo llega a ~USD 2,000, no vender "todo el sistema". Vender etapa inicial acotada + continuidad por fases.

---

## 8) Frases de alineacion para usar en la reunion
- "No estamos vendiendo software infinito, estamos vendiendo una primera etapa rentable."
- "Si el ticket inicial es bajo, el valor se captura en fases y en continuidad."
- "El cliente es dueno de sus datos; nosotros cuidamos el core para escalar."
- "La propuesta tiene que cerrar comercialmente hoy y tecnicamente manana."

---

## 9) Proximo paso recomendado despues de la reunion
1. Actualizar `proyecto-consolidado-final.md` con los acuerdos reales.
2. Generar `propuesta-comercial-cliente.md` en version corta.
3. Generar `presupuesto-v1.md` con montos y hitos.
4. Enviar al cliente y agendar reunion de validacion.
