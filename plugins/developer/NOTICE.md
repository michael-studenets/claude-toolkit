# Attribution

The skills, hook and scripts in this plugin are adapted from
[Superpowers](https://github.com/obra/superpowers) by Jesse Vincent
(commit `8ca22db`, v6.4.2), used under the MIT License (see `LICENSE`).

Changes from upstream:

- Only the skills needed for the spec → plan → implementation workflow are included.
- `using-git-worktrees` dropped: work happens on a regular feature branch.
- Skill namespace `superpowers:` renamed to `developer:`; `using-superpowers` renamed to `using-developer`.
- Default artifact paths: `docs/developer/specs/`, `docs/developer/plans/`, `.developer/` (instead of `docs/superpowers/…`, `.superpowers/`).
- Non-Claude-Code platform adapters removed from the session-start hook and `using-developer`.
- Brainstorming visual companion no longer loads a remote logo image.
- Added `/developer:spec`, `/developer:plan`, `/developer:implement` commands.
