---
name: crear-harness
description: Guía a la persona, paso a paso, para armar el harness de su propio proyecto dentro de mi-harness/. Pregunta de a una cosa por vez y crea solo los archivos y carpetas que cada respuesta necesita. Retoma si quedó a medias. Usar cuando digan "crear harness", "armar mi harness", "empezar el taller" o "seguir con mi harness".
---

# Crear un harness

Un **harness** es la capa que rodea a un modelo y lo convierte en un agente: el ciclo de trabajo, las herramientas, el contexto, los permisos y la evidencia con la que demuestra que terminó. Tu trabajo es ayudar a la persona a armar el de **su** proyecto, entendiendo cada pieza mientras la construye.

Las piezas, con ejemplos, están en `references/componentes.md`. Leelo antes de empezar.

## Reglas

1. **Una pregunta por vez.** Esperá la respuesta antes de seguir. Si la persona no sabe qué contestar, dale dos o tres ejemplos concretos para su caso.
2. **Nada vacío.** Creá un archivo o una carpeta solo cuando una respuesta le da contenido. Si una pieza no hace falta, decí por qué y seguí: una ausencia decidida también es una decisión.
3. **Con sus palabras.** Escribí lo que la persona dijo, ordenado. No inventes comandos, rutas ni reglas que no salieron de la conversación. Si falta un dato, preguntalo.
4. **Mostrá lo que creaste.** Después de cada paso, listá los archivos nuevos o cambiados y en una línea qué pieza del harness cubren.
5. **Todo va en `mi-harness/`.** No toques los archivos del taller.
6. **Llevá el estado.** Al cerrar cada paso, actualizá `mi-harness/ESTADO.md` (formato abajo).
7. **Explicá el porqué.** Antes de cada paso, una o dos frases sobre qué problema resuelve esa pieza. Es un taller: que se entienda, no solo que quede hecho.

## Al empezar

- Si existe `mi-harness/ESTADO.md`, leelo, resumí en tres líneas dónde quedó y preguntá si sigue desde ahí o quiere revisar un paso anterior.
- Si no existe, presentá el proceso en una lista corta (los ocho pasos de abajo) y arrancá por el paso 1.

## Los pasos

### 1. El problema

Preguntá, de a una:

- ¿Qué tarea querés que haga el agente? Pedí un ejemplo real, no una categoría.
- ¿Qué sale mal hoy cuando se la pedís a un agente, o qué te da miedo que salga mal?
- ¿Dónde vive el trabajo? (un repo, una carpeta, un sistema como Odoo, documentos…)

Creá `mi-harness/AGENTS.md` con una sección **Qué es este proyecto** y otra **Qué sale mal hoy**. Esa lista de problemas guía el resto: en cada paso siguiente, señalá cuál de esos problemas ataca.

### 2. La tarea: qué es "terminado"

- ¿Cómo te das cuenta de que una tarea quedó bien hecha?
- ¿Qué no puede romperse mientras tanto?

Sumá a `AGENTS.md` la sección **Cuándo una tarea está terminada**, como lista de requisitos que se puedan comprobar. Si la persona contesta algo vago ("que ande"), ayudala a bajarlo a algo observable.

### 3. Contexto y memoria

- ¿Qué tendría que saber alguien nuevo antes de tocar algo? (estructura, convenciones, nombres, decisiones tomadas)
- ¿Qué errores ya conocés, que se repiten?

Lo corto y que vale siempre va en `AGENTS.md`, sección **Contexto**. Si hay mucho, o son temas separados, creá `mi-harness/memoria/` con un archivo por tema (por ejemplo `convenciones.md`, `fallas-conocidas.md`) y enlazalos desde `AGENTS.md`. `AGENTS.md` tiene que poder leerse entero en un par de minutos.

### 4. Herramientas

- ¿Qué comandos usás para correr, probar o revisar el trabajo? Pedí los comandos exactos.
- ¿Necesita consultar o modificar algún sistema externo? (una base, una API, Odoo, Slack…)

Comandos: sección **Herramientas** en `AGENTS.md`, uno por línea, con qué hace cada uno. Sistemas externos: anotá en `AGENTS.md` qué necesita y para qué. Si la persona ya tiene un servidor MCP para ese sistema, creá `mi-harness/.mcp.json` con lo que ella te dé; si no, dejalo anotado como pendiente en `ESTADO.md`. No inventes configuraciones.

### 5. Permisos

Preguntá en tres partes:

- ¿Qué puede hacer solo, sin preguntarte?
- ¿Qué tiene que pedirte antes? (publicar, mandar mensajes, borrar, gastar…)
- ¿Qué no tiene que hacer nunca?

Creá `mi-harness/.claude/settings.json` con `permissions.allow`, `permissions.ask` y `permissions.deny`, solo con lo que se pueda expresar como regla de herramienta (por ejemplo `"Bash(rm -rf:*)"` en `deny`). Lo que no se pueda expresar así va como regla escrita en `AGENTS.md`, sección **Límites**. Explicá la diferencia: una regla en un archivo de configuración se cumple siempre; una regla en texto depende de que el modelo la respete.

### 6. Procedimientos

- ¿Hay pasos que repetís siempre igual? (preparar un entorno, publicar, revisar algo antes de entregar)

Por cada procedimiento que valga la pena, creá `mi-harness/.claude/skills/<nombre-en-kebab>/SKILL.md` con `name`, `description` (cuándo usarla) y los pasos. Si no hay ninguno, no crees la carpeta.

Preguntá también si hay algo que quiera que pase **siempre** en un momento fijo (por ejemplo, correr el linter después de cada edición). Si lo hay, eso es un hook: sumalo a `.claude/settings.json` y explicá que, a diferencia de una instrucción, lo ejecuta el harness y no depende del modelo.

### 7. Verificación

- Para cada requisito del paso 2: ¿cómo se comprueba? (un test, un comando, algo que se mira)

Creá `mi-harness/verificacion/checklist.md`: una fila por requisito, con cómo se comprueba. Sumá a `AGENTS.md` la regla: **antes de decir que terminó, recorré `verificacion/checklist.md` y mostrá la evidencia de cada punto**. "Listo, funciona" no es evidencia.

### 8. Síntomas y medidas

Explicá la idea: cada vez que la persona tiene que intervenir (decirle qué archivo mirar, interpretarle un error, verificar a mano, limpiar lo que dejó), está tapando una pieza que falta.

Creá `mi-harness/sintomas/intervenciones.md` con esta tabla vacía y una fila de ejemplo tachada:

| Fecha | Qué tuve que hacer | Qué faltaba | Qué cambio en el harness |
| --- | --- | --- | --- |

Y la guía para clasificar lo que faltaba: contexto, herramienta, permisos, verificación, recuperación ante un error, limpieza, o el modelo mismo.

## Cierre

1. Mostrá el árbol de `mi-harness/` y, para cada archivo, qué pieza cubre.
2. Decí en qué nivel quedó:
   - **Base**: solo la tarea y los archivos.
   - **Herramientas**: + comandos y permisos.
   - **Contexto**: + memoria del proyecto y estado.
   - **Verificación**: + checklist con evidencia.
3. Proponé el próximo paso concreto: usar el harness en una tarea real y anotar cada intervención en `sintomas/intervenciones.md`.
4. Explicá cómo probarlo: `cd mi-harness` y abrir el agente ahí.

## Formato de `mi-harness/ESTADO.md`

```markdown
# Estado del harness

Último paso cerrado: <número y nombre>
Próximo paso: <número y nombre>

## Decisiones
- <pieza>: <qué se decidió, o "no hace falta porque…">

## Pendientes
- <lo que quedó para después>
```
