# claude-toolkit

Мій особистий маркетплейс плагінів для [Claude Code](https://claude.com/claude-code).

## Встановлення

```bash
/plugin marketplace add michael-studenets/claude-toolkit
/plugin install developer@claude-toolkit
```

## Плагіни

| Плагін | Опис |
|--------|------|
| [`developer`](plugins/developer) | Процес розробки: спека → план → реалізація (TDD, субагенти, код-рев'ю). Побудований на скілах [Superpowers](https://github.com/obra/superpowers). |

## Плагін `developer`

### Процес

```
/developer:spec <ідея>      → brainstorming      → docs/developer/specs/YYYY-MM-DD-<topic>-design.md
/developer:plan [спека]     → writing-plans      → docs/developer/plans/YYYY-MM-DD-<feature>.md
/developer:implement [план] → subagent-driven-development (або executing-plans)
                           ├─ test-driven-development      RED → GREEN → REFACTOR на кожне завдання
                           ├─ requesting/receiving-code-review  рев'ю після кожного завдання
                           ├─ verification-before-completion    докази перед «готово»
                           └─ finishing-a-development-branch    merge / PR / залишити
```

Команди — лише зручні точки входу: скіли спрацьовують і самі, бо SessionStart-хук
підвантажує `using-developer`, який змушує Claude перевіряти й використовувати доречні скіли.

### Скіли

| Етап | Скіл | Навіщо |
|------|------|--------|
| Bootstrap | `using-developer` | Правила пошуку й використання скілів (інжектиться хуком на старті сесії) |
| Спека | `brainstorming` | Діалог з уточненнями → узгоджений дизайн → спека + рев'ю спеки |
| План | `writing-plans` | Детальний план з дрібними TDD-завданнями, точними файлами й тестами |
| Реалізація | `subagent-driven-development` | Свіжий субагент на кожне завдання + рев'ю після кожного |
| Реалізація | `executing-plans` | Виконання плану в поточній сесії (без субагентів) |
| Реалізація | `dispatching-parallel-agents` | Паралельні незалежні завдання |
| Якість | `test-driven-development` | Спершу падаючий тест, потім код |
| Якість | `systematic-debugging` | Пошук першопричини замість вгадування фіксів |
| Якість | `requesting-code-review` / `receiving-code-review` | Рев'ю субагентом і тверезе опрацювання зауважень |
| Якість | `verification-before-completion` | Жодних заяв «працює» без запуску перевірок |
| Завершення | `finishing-a-development-branch` | Merge, PR, або збереження гілки |

Зі Superpowers свідомо **не** взято: `writing-skills` (створення скілів),
`diagnosing-superpowers` (діагностика самого Superpowers) та `using-git-worktrees`
(робота ведеться у звичайній feature-гілці).

### Артефакти в проєкті

- `docs/developer/specs/` — спеки (комітяться)
- `docs/developer/plans/` — плани (комітяться)
- `.developer/` — робочі файли субагентів і візуального компаньйона (додайте в `.gitignore`)

## Ліцензія

Скіли адаптовано з [obra/superpowers](https://github.com/obra/superpowers) (MIT, © Jesse Vincent).
Див. [`plugins/developer/LICENSE`](plugins/developer/LICENSE) і [`plugins/developer/NOTICE.md`](plugins/developer/NOTICE.md).
