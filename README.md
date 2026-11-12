# krlsstack

Stack personal y portable de workflow de IA para [OpenCode](https://opencode.ai): una skill que convierte al modelo principal en un orquestador de ingeniería rigurosa y un subagente que ejecuta el código.

**Inspirado en [pstack](https://github.com/painhardcore/pstack)** (la adaptación portable del plugin pstack de Cursor para Codex, Claude Code y OpenCode). krlsstack sigue la misma idea — workflows como skills y agentes versionados en un repo, fáciles de instalar en cualquier máquina — pero con un stack propio y mínimo, en español.

## Contenido

| Tipo | Nombre | Qué hace |
| --- | --- | --- |
| Skill | `krls-mode` | Modo de ingeniería rigurosa. Convierte al modelo principal en orquestador: clasifica la tarea, elige playbook (feature / investigation / solve), delega la escritura de código y verifica con evidencia real. |
| Agente | `worker` | Subagente de krls-mode para escritura de código y exploración pesada. Lee el manual de krls-mode antes de trabajar, respeta el scope del brief y reporta PASS / ISSUES / BLOCKED con evidencia. |

No hay agente orquestador aparte: el orquestador es el modelo principal de la sesión y su comportamiento lo define la skill `krls-mode`.

## Estructura

```
krlsstack/
├── agents/
│   └── worker.md                     # subagente de ejecución
└── skills/
    └── krls-mode/
        ├── SKILL.md                  # manual del orquestador
        └── playbooks/
            ├── feature.md            # comportamiento nuevo o cambiado
            ├── investigation.md      # preguntas de solo lectura
            └── solve.md              # defectos y refactors
```

## Instalación (OpenCode)

Clona el repo y copia las carpetas a tu config global de OpenCode:

```sh
git clone https://github.com/KrlsDev/krlsstack.git
cd krlsstack

mkdir -p ~/.config/opencode/skills ~/.config/opencode/agents
cp -R skills/krls-mode ~/.config/opencode/skills/krls-mode
cp agents/worker.md ~/.config/opencode/agents/worker.md
```

Arranca una sesión nueva de OpenCode y ya están disponibles.

### Instalación por proyecto

Para llevar el stack a un proyecto concreto en vez de a tu usuario:

```sh
mkdir -p .opencode/skills .opencode/agents
cp -R /ruta/a/krlsstack/skills/krls-mode .opencode/skills/krls-mode
cp /ruta/a/krlsstack/agents/worker.md .opencode/agents/worker.md
```

## Uso

1. **Requisito por proyecto:** krls-mode exige una skill de verificación local llamada siempre `verify` en `.opencode/skills/verify/` (cómo lanzar la app, diagnóstico read-only, qué evidencia capturar y cleanup). Sin ella, el orquestador reporta `SETUP INCOMPLETO` y no arranca ningún playbook. Opcionalmente, una skill `krls-git` en `.opencode/skills/` para convenciones de commits y ramas.
2. **Invoca el modo:** escribe `@krls-mode` seguido de la tarea (feature, bug, investigación…). Solo el usuario puede invocarla; el modelo no la activa por su cuenta.
3. **Flujo:** el orquestador clasifica la tarea, abre la todolist con el playbook, y delega toda escritura de código al agente `worker` en background con un brief standalone. Revisa el diff real, verifica en la superficie real (app, tests, CLI) y reporta con evidencia pegada.

Para sincronizar cambios entre máquinas: edita en una, `git pull` en la otra, y vuelve a copiar (o mejor, clona y enlaza con symlinks).

## Créditos

Estructura e idea inspiradas en [painhardcore/pstack](https://github.com/painhardcore/pstack), adaptación portable del [plugin pstack de Cursor](https://github.com/cursor/plugins/tree/main/pstack).
