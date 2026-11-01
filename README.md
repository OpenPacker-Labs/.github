# OpenPacker-Labs/.github

Default community health files and org-wide agent skills for
[OpenPacker-Labs](https://github.com/OpenPacker-Labs) repositories.

| Content | Purpose |
| --- | --- |
| `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md` | Org default community files (inherited by member repos) |
| `ISSUE_TEMPLATE/`, `.github/pull_request_template.md` | Default issue and PR templates |
| `.agents/skills/`, `.claude/skills/`, `.claude/agents/` | SDLC coordinator, gh-stack, implementer/reviewer backends |
| `AGENTS.md` | Skill install map and OpenPacker sdlc binding |
| `scripts/check-skill-mirrors.mjs` | Byte-identical mirror check for `.agents` / `.claude` skills |

Install skills into a project checkout with
[`OpenPacker-Labs/dotfiles`](https://github.com/OpenPacker-Labs/dotfiles).
