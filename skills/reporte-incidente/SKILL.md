---
name: reporte-incidente
description: Redacta el reporte formal de un incidente a partir de un ticket de TicketOps (resumen, impacto, línea de tiempo desde el historial, causa probable, acciones tomadas y preventivas). Úsalo cuando pidan un reporte, informe o post mortem de un incidente, caída o ticket crítico, por ejemplo para el supervisor o el comité.
---

# Reporte de incidente

Produce un reporte de incidente formal, breve y en español neutro a partir de un ticket de TicketOps.

## Entradas

Usa, en este orden, lo que esté disponible:

1. Los datos que da el pedido (prioridad, categoría, descripción, duración, causa).
2. El ticket de la API si se indica un ID: `GET /tickets/:id` y `GET /tickets/:id/historial` (`historial` trae `event`, `from`, `to`, `at`, `author`, `detail`).
3. Si falta un dato, escribe «No informado». **Nunca inventes** horas, nombres, cifras de impacto ni causas.

## Reglas de redacción

- Tono formal y breve: cada sección de 1 a 4 líneas o viñetas.
- Español neutro, sin tecnicismos innecesarios. A quienes reportan se les dice «solicitantes», nunca «usuarios».
- Horas en formato `HH:MM` y duraciones como «3 h 20 min».
- No incluyas datos personales más allá del nombre del solicitante y del agente. No incluyas secretos ni contenido de archivos `.env`.
- La causa se presenta como «probable» salvo que el pedido la confirme.
- SLA de referencia: CRITICA 4 h, ALTA 8 h, MEDIA 24 h, BAJA 72 h. Indica si se cumplió.

## Formato de salida

Responde exactamente con esta estructura en Markdown:

```markdown
# Reporte de incidente — <ID o título breve>

| Campo | Valor |
|-------|-------|
| Ticket | <ID o «No informado»> |
| Categoría | <categoría> |
| Prioridad | <prioridad> (SLA <n> h) |
| Duración | <tiempo hasta resolver> |
| SLA | Cumplido / Incumplido por <tiempo> |
| Estado | <estado actual> |

## Resumen
<Qué pasó, en 1 a 3 oraciones.>

## Impacto
<A quién y a qué afectó, y durante cuánto tiempo.>

## Línea de tiempo
| Hora | Evento |
|------|--------|
| HH:MM | <evento del historial o del pedido> |

## Causa probable
<Causa técnica en lenguaje claro.>

## Acciones tomadas
- <acción>

## Acciones preventivas
- <acción concreta, con responsable sugerido por rol, no por nombre>
```

## Línea de tiempo desde el historial

Convierte cada entrada del historial en una fila:

| `event` | Texto |
|---------|-------|
| `CREADO` | «Se registra el ticket (solicitante: <author>).» |
| `CAMBIO_ESTADO` a `ASIGNADO` | «Se asigna a <detail>.» |
| `CAMBIO_ESTADO` a `EN_PROGRESO` | «Comienza la atención.» o «Se retoma la atención.» si venía de `EN_ESPERA` o `RESUELTO` |
| `CAMBIO_ESTADO` a `EN_ESPERA` | «Queda en espera (SLA en pausa).» |
| `CAMBIO_ESTADO` a `RESUELTO` | «Se resuelve: <detail>.» |
| `CAMBIO_ESTADO` a `CERRADO` | «Se cierra el ticket.» |
| `ESCALADO` | «Vence el SLA; se notifica al supervisor.» |
| `REASIGNADO` | «Se reasigna (<detail>).» |

Si no hay historial y el pedido solo da la duración, arma la línea de tiempo con inicio, resolución y los hitos que se mencionen.
