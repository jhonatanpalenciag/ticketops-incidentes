# Power `ticketops-incidentes`

Power de Kiro para TicketOps: redacta reportes de incidentes a partir de tickets operacionales y orienta el escalamiento cuando se vence un SLA. Sigue la especificación [Agent Plugins](https://agent-plugins.org).

## Contenido

```
ticketops-incidentes/
├── plugin.json                       # manifiesto y palabras clave de activación
├── mcp.json                          # servidor MCP fetch (uvx mcp-server-fetch)
└── skills/
    └── reporte-incidente/SKILL.md    # Resumen, Impacto, Línea de tiempo, Causa probable, Acciones tomadas y preventivas
```

## Activación

Se activa cuando la conversación menciona: `ticket`, `incidente`, `sla`, `escalamiento` o `reporte de incidente`. Las herramientas del servidor `fetch` solo se cargan con el power activo.

## Instalación

- **Desde una carpeta:** Kiro → panel *Powers* → *Add Custom Power* → *Import power from a folder* → elige esta carpeta.
- **Desde GitHub:** *Add Custom Power* → *Import power from GitHub* → URL del repositorio.

## Requisitos

- `uv` / `uvx` para el servidor MCP `fetch`.

Todos los ejemplos usan datos ficticios.
