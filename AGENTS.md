# Agent instructions (OpenPacker-Labs)

Org-wide skills and agent backends for OpenPacker and sibling repositories.
Product-specific gates and protocol boundaries for the PREX reference
implementation remain in
[`OpenPacker` `AGENTS.md`](https://github.com/OpenPacker-Labs/OpenPacker/blob/main/AGENTS.md).

Install these trees into a checkout with
[`OpenPacker-Labs/dotfiles` `install.sh`](https://github.com/OpenPacker-Labs/dotfiles/blob/main/install.sh)
(devcontainer, Codespaces, or local).

## Installed skills

| Skill        | Path (mirrors)                                        | Use                                                                                                                          |
| ------------ | ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **sdlc**     | `.agents/skills/sdlc` ≡ `.claude/skills/sdlc`         | Full loop: brainstorm → plan → issues → subagents → stacked PRs → bottom-up review → squash-merge. `/sdlc`, `/sdlc --finish` |
| **gh-stack** | `.agents/skills/gh-stack` ≡ `.claude/skills/gh-stack` | Non-interactive `gh stack` CLI for stacked PRs                                                                               |

Keep skill mirrors byte-identical: `node scripts/check-skill-mirrors.mjs`.

Subagent definitions for the Claude Code backend:

- `.claude/agents/implementer.md` — one issue, one worktree, incremental commits
- `.claude/agents/reviewer.md` — read-only gate + acceptance re-check

## OpenPacker sdlc binding

The **sdlc** skill is bound to [`OpenPacker`](https://github.com/OpenPacker-Labs/OpenPacker):

1. Durable state: `docs/plans/<initiative-slug>/sdlc-state.md` (in OpenPacker)
2. Dispatch log: `docs/plans/dispatch-log.md`
3. Handback: `.sdlc/report.json` (worktree) or fenced `sdlc-report` on cloud PRs
4. Gates: narrow workspace checks per commit; **`npm run verify`** before PR/merge
5. Stacks: `gh stack` (`github/gh-stack`); bottom-up squash-merge closeout
6. Billing-only CI red does not block squash-merge (document on PR + state file)

See `.agents/skills/sdlc/SKILL.md` § **OpenPacker binding** for HoBo → OpenPacker
command mapping. Draft-proof cascade / Linear are optional; use ADRs +
`spec/prex/v1` when draft/Linear are not in use.

## Git defaults (local)

```bash
git config --local rerere.enabled true
git config --local remote.pushDefault origin
gh extension install github/gh-stack # if missing
```

Use the GitHub connector for GitHub API work when available. Preserve unrelated
user changes; fetch `origin/main` before publishing stacks; never force-push
`main`.
