# Attribution

The skills, hook and scripts in this plugin are adapted from
[Superpowers](https://github.com/obra/superpowers) by Jesse Vincent
(commit `8ca22db`, v6.4.2), used under the MIT License (see `LICENSE`).

Changes from upstream:

- Only the skills needed for the spec → plan → implementation workflow are included.
- Skill namespace `superpowers:` renamed to `agent:`; `using-superpowers` renamed to `using-agent`.
- Default artifact paths: `docs/agent/specs/`, `docs/agent/plans/`, `.agent/` (instead of `docs/superpowers/…`, `.superpowers/`).
- Non-Claude-Code platform adapters removed from the session-start hook and `using-agent`.
- Brainstorming visual companion no longer loads a remote logo image.
- Added `/agent:spec`, `/agent:plan`, `/agent:implement` commands.
