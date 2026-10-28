# Taller: armá tu harness

Un agente es **modelo + harness**. El modelo piensa; el harness es todo lo demás: el contexto que ve, las herramientas que usa, los permisos que tiene y la forma en que demuestra que terminó.

Este repo te guía para armar el harness de **tu** proyecto, paso a paso. No trae nada hecho: lo vas creando vos, respondiendo preguntas.

## Qué necesitás

- Un agente que lea skills, por ejemplo [Claude Code](https://docs.claude.com/en/docs/claude-code).
- Un proyecto o una tarea concreta en la que quieras que el agente te ayude.

## Cómo se usa

```bash
git clone <url-de-este-repo>
cd taller-harness
claude
```

Adentro del agente, escribí:

```
/crear-harness
```

La skill te va a preguntar, de a una cosa por vez:

1. **El problema**: qué tarea querés delegar y qué falla hoy.
2. **La tarea**: qué es "terminado" para vos.
3. **Contexto y memoria**: qué tiene que saber el agente de tu proyecto.
4. **Herramientas**: qué comandos y sistemas necesita.
5. **Permisos**: qué puede hacer solo, qué tiene que preguntar y qué nunca.
6. **Procedimientos**: qué pasos repetís siempre igual.
7. **Verificación**: cómo demuestra que cumplió.
8. **Síntomas y medidas**: cómo vas a saber qué le falta.

Con cada respuesta crea solo los archivos y carpetas que hacen falta, dentro de `mi-harness/`. Si cortás a la mitad, la próxima vez que la lances retoma desde donde quedaste.

Al final, abrí tu harness y probalo:

```bash
cd mi-harness
claude
```

## Con otro agente

Si tu agente no tiene el comando `/crear-harness`, pedile:

> Leé `.claude/skills/crear-harness/SKILL.md` y seguilo paso a paso.

## Qué hay en el repo

| Archivo | Para qué |
| --- | --- |
| `.claude/skills/crear-harness/SKILL.md` | La skill que guía el proceso |
| `.claude/skills/crear-harness/references/componentes.md` | Las piezas de un harness, explicadas |
| `AGENTS.md` | Instrucciones para el agente que corre el taller |
