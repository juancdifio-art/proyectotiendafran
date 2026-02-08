# Comparativa: `byme` vs `main`

## Objetivo
Comparar los documentos de brainstorming y quedarnos con una sola linea para presentar una propuesta por fases (tecnica + economica) el martes.

## Fuentes revisadas
- `proyectotiendafran-byme/chat-1.md`
- `proyectotiendafran-byme/chat-2-md`
- `proyectotiendafran-main/docs de inicio/beluga.md`
- `proyectotiendafran-main/docs de inicio/chatgpt52.md`
- `proyectotiendafran-main/docs de inicio/geminiflash3.md`
- `proyectotiendafran-main/docs de inicio/glm46.md`
- `proyectotiendafran-main/docs de inicio/propuesta-unificada.md`

## Lo mejor de `byme`
- Estrategia de producto correcta: empezar por `single-store` y escalar despues.
- Buen recorte de MVP para vender rapido sin sobredisenar.
- PRD muy util para ejecucion (requisitos, estados, criterios de aceptacion).
- Arquitectura alineada al stack del equipo (PERN + Next).
- Define bien que NO entra en Fase 1 (evita desbordes).

## Lo mejor de `main`
- Mejor forma de contar el valor de negocio al cliente (stock unico, menos WhatsApp, propiedad de datos).
- Mejor armado comercial: hitos, anticipo, garantia, mantenimiento, riesgos.
- Incluye opcion de Discovery pago (muy util para cerrar formalmente).
- Incluye rangos de inversion y modalidades de contratacion.

## Riesgos detectados (si se usa `main` sin ajustes)
- Alcance inicial demasiado grande (2 apps + gestion completa + pagos + stock avanzado).
- Puede generar promesas altas en tiempo/costo para una primera etapa.
- Mezcla de stacks (Laravel/Flutter/Node/etc.) sin anclar al stack real del equipo.
- Parte de valores en ARS estan desactualizados para usar "tal cual".

## Decision recomendada
Usar una propuesta hibrida:
1. Base de producto y fases desde `byme`.
2. Estructura comercial y contractual desde `main`.
3. Modelo economico por etapas: Discovery -> Fase 1 -> Fase 1.5 -> Fase 2.
4. Marketplace solo como vision futura (Fase 3), no como compromiso inmediato.

## Mensaje clave para el cliente
"Primero resolvemos ventas online del local con operacion estable. Despues, con la base ya funcionando, incorporamos mayorista y automatizaciones avanzadas."
