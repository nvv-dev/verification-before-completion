# verification-before-completion

> "Listo" es una afirmación, y necesita evidencia.

**Verificación antes de cerrar** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Antes de decir que algo está terminado, el agente corre las verificaciones después de su último cambio, las compara con cada criterio de aceptación y lista por nombre todo lo que debilitó: pruebas omitidas, timeouts ampliados, advertencias silenciadas. Si algo no se puede verificar en ese entorno (un dispositivo, una firma), lo dice y explica cómo correrlo.

## Objetivo

Que los resúmenes de los agentes sean confiables y que nada se dé por hecho sin prueba.

## Cuándo usarla

- Antes de un commit, un PR o un resumen final
- Al cerrar cualquier tarea

## Cuándo no

- Preguntas o exploración sin cambios

## Ejemplo

```text
Termina la tarea y entrégame el reporte de verificación.
```

## Cómo se activa

Esta skill **se activa sola**: Claude Code lee su descripción y la carga cuando la tarea coincide. También puedes pedirla por nombre ("usa la skill verification-before-completion") o invocarla con `/verification-before-completion:verification-before-completion` (plugin) o `/verification-before-completion` (copiada a `.claude/skills/`).

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install verification-before-completion@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `dev-workflow@nvvdev` en su lugar (incluye esta skill y las demás de [dev-workflow](https://github.com/nvv-dev/dev-workflow)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/verification-before-completion.git /tmp/verification-before-completion
mkdir -p .claude/skills
cp -R /tmp/verification-before-completion/skills/verification-before-completion .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/verification-before-completion/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/verification-before-completion
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `verification-before-completion` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall verification-before-completion@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/verification-before-completion`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/verification-before-completion/SKILL.md`](skills/verification-before-completion/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/verification-before-completion/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [obra/superpowers](https://github.com/obra/superpowers) (verification-before-completion), [garrytan/gstack](https://github.com/garrytan/gstack) (/review, /qa).

## Licencia

MIT.

---

## English

**verification-before-completion** — Fresh evidence after the last change, checked against each acceptance criterion, plus an honest list of what was weakened or skipped.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install verification-before-completion@nvvdev`, or copy `skills/verification-before-completion/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/verification-before-completion`. Loads automatically when the task matches its description. Canonical source: [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow). License: MIT.
