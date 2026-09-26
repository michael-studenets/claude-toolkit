---
description: Execute an implementation plan task by task with TDD and code review
argument-hint: [path to plan]
---

Execute this implementation plan:

$ARGUMENTS

If no plan path is given, use the most recent plan in `docs/developer/plans/` and confirm the choice with me first.

Use the `developer:subagent-driven-development` skill (fresh subagent per task, review after each task). If I ask for inline execution or no subagent tool is available, use `developer:executing-plans` instead. Follow the chosen skill exactly, including `developer:test-driven-development`, `developer:verification-before-completion` and `developer:finishing-a-development-branch`.
