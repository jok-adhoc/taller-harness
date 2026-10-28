# Las piezas de un harness

**Agente = modelo + harness.** El harness es la capa de software que rodea a un modelo de lenguaje y lo convierte en un agente: administra el ciclo de trabajo, las herramientas que puede usar, el contexto que ve, los permisos que tiene y la evidencia con la que demuestra que terminó.

Tres rasgos:

- **Está afuera del modelo.** Con el mismo modelo, otro harness da otro resultado.
- **Gobierna la tarea entera,** desde el pedido hasta que demuestra que terminó.
- **Deja evidencia:** qué miró, qué hizo, qué probó y dónde necesitó ayuda.

## El problema que resuelve

Un buen modelo igual falla la tarea: mira los archivos equivocados, corre los tests que no son, arregla una parte y rompe otra, dice "listo" sin probar. Hoy esos huecos los tapa una persona, a mano. El harness los cubre de forma explícita.

## Las siete piezas

| Pieza | Qué resuelve | Ejemplo | Dónde queda en el taller |
| --- | --- | --- | --- |
| Loop | Decide el próximo paso y cuándo parar | Pensar → actuar → mirar el resultado | Lo trae el agente (Claude Code, Codex…) |
| Conexión con el modelo | Hablar con el modelo y armar el pedido | Elegir modelo, caché | Lo trae el agente |
| Herramientas | Lo que el agente puede hacer | Editar archivos, correr comandos, consultar un sistema | `AGENTS.md` › Herramientas, `.mcp.json` |
| Memoria y contexto | Que sepa dónde mirar y no redescubra todo | Convenciones, errores conocidos | `AGENTS.md` › Contexto, `memoria/` |
| Seguridad y permisos | Qué corre solo, qué pide permiso, qué nunca | Prohibir borrados, pedir antes de publicar | `.claude/settings.json`, `AGENTS.md` › Límites |
| Orquestación | Repartir trabajo entre agentes | Sub-agentes que exploran en paralelo | No hace falta para empezar |
| Extensibilidad | Sumar capacidades | Skills, hooks, MCP | `.claude/skills/`, hooks en `.claude/settings.json` |

Y dos que cierran el circuito:

- **Verificación:** cada requisito con su prueba. Queda en `verificacion/checklist.md`.
- **Síntomas y medidas:** registrar cada intervención y qué pieza faltaba. Queda en `sintomas/intervenciones.md`.

## Regla en texto o regla en configuración

- **En texto** (`AGENTS.md`, una skill): el modelo la lee y en general la respeta, pero puede olvidarla.
- **En configuración** (permisos, hooks): la aplica el harness, siempre.

Lo crítico va en configuración. Lo que necesita criterio va en texto.

## Los cuatro niveles

| Nivel | Qué tiene |
| --- | --- |
| Base | La tarea y los archivos |
| Herramientas | + comandos, permisos |
| Contexto | + memoria del proyecto, estado de la tarea |
| Verificación | + chequeos con evidencia antes de decir "terminé" |

## Síntomas: qué te dice cada intervención

| Tuviste que… | Faltaba |
| --- | --- |
| Decirle qué archivo mirar | Contexto |
| Interpretarle un error | Herramientas o salida legible |
| Verificar el resultado a mano | Verificación |
| Limpiar lo que dejó | Reglas de limpieza |
| Frenarlo antes de algo riesgoso | Permisos |

Medir es simple: **contá** cada intervención, **clasificala** según la tabla y **exigí evidencia** al cerrar cada tarea.
