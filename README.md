# claude-toolkit

Мій особистий маркетплейс плагінів для [Claude Code](https://claude.com/claude-code).

## Встановлення

```bash
/plugin marketplace add michael-studenets/claude-toolkit
/plugin install agent@claude-toolkit
```

## Плагіни

| Плагін | Опис |
|--------|------|
| [`agent`](plugins/agent) | Процес розробки: спека → план → реалізація (TDD, субагенти, код-рев'ю). Побудований на скілах [Superpowers](https://github.com/obra/superpowers). |

## Плагін `agent`

### Процес

```
/agent:spec <ідея>      → brainstorming      → docs/agent/specs/YYYY-MM-DD-<topic>-design.md
/agent:plan [спека]     → writing-plans      → docs/agent/plans/YYYY-MM-DD-<feature>.md
/agent:implement [план] → subagent-driven-development (або executing-plans)
                           ├─ using-git-worktrees          ізольоване робоче дерево
                           ├─ test-driven-development      RED → GREEN → REFACTOR на кожне завдання
                           ├─ requesting/receiving-code-review  рев'ю після кожного завдання
                           ├─ verification-before-completion    докази перед «готово»
                           └─ finishing-a-development-branch    merge / PR / залишити
```

Команди — лише зручні точки входу: скіли спрацьовують і самі, бо SessionStart-хук
підвантажує `using-agent`, який змушує Claude перевіряти й використовувати доречні скіли.

### Скіли

| Етап | Скіл | Навіщо |
|------|------|--------|
| Bootstrap | `using-agent` | Правила пошуку й використання скілів (інжектиться хуком на старті сесії) |
| Спека | `brainstorming` | Діалог з уточненнями → узгоджений дизайн → спека + рев'ю спеки |
| План | `writing-plans` | Детальний план з дрібними TDD-завданнями, точними файлами й тестами |
| Реалізація | `subagent-driven-development` | Свіжий субагент на кожне завдання + рев'ю після кожного |
| Реалізація | `executing-plans` | Виконання плану в поточній сесії (без субагентів) |
| Реалізація | `dispatching-parallel-agents` | Паралельні незалежні завдання |
| Реалізація | `using-git-worktrees` | Ізоляція роботи в окремому worktree |
| Якість | `test-driven-development` | Спершу падаючий тест, потім код |
| Якість | `systematic-debugging` | Пошук першопричини замість вгадування фіксів |
| Якість | `requesting-code-review` / `receiving-code-review` | Рев'ю субагентом і тверезе опрацювання зауважень |
| Якість | `verification-before-completion` | Жодних заяв «працює» без запуску перевірок |
| Завершення | `finishing-a-development-branch` | Merge, PR, або збереження гілки |

Зі Superpowers свідомо **не** взято: `writing-skills` (створення скілів) та
`diagnosing-superpowers` (діагностика самого Superpowers) — вони не потрібні для
процесу спека → план → реалізація.

### Артефакти в проєкті

- `docs/agent/specs/` — спеки (комітяться)
- `docs/agent/plans/` — плани (комітяться)
- `.agent/` — робочі файли субагентів і візуального компаньйона (додайте в `.gitignore`)

## Ліцензія

Скіли адаптовано з [obra/superpowers](https://github.com/obra/superpowers) (MIT, © Jesse Vincent).
Див. [`plugins/agent/LICENSE`](plugins/agent/LICENSE) і [`plugins/agent/NOTICE.md`](plugins/agent/NOTICE.md).
