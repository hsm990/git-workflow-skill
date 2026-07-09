# git-workflow

An [Agent Skill](https://github.com/anthropics/skills) that teaches your AI coding
tool a professional, solo-friendly git workflow: never commit to `main`, use
`feature/fix/chore` branches, Conventional Commits, PR + squash-merge.

Once installed, just talk to your agent normally — "commit this", "push this",
"start working on the hero section" — and it will follow the workflow
automatically: check if you're on `main`, branch off if needed, commit with a
proper conventional message, push the branch (never `main`), and open a PR.

## What's inside

```
git-workflow/
├── SKILL.md              # the skill itself — workflow rules, commands, recipes
├── scripts/
│   └── new-branch.sh     # helper: safely branch off if currently on main
├── .claude/INSTALL.md    # agent-executable install steps for Claude Code
├── .codex/INSTALL.md     # agent-executable install steps for Codex CLI
├── .opencode/INSTALL.md  # agent-executable install steps for OpenCode
├── .cursor/INSTALL.md    # agent-executable install steps for Cursor
├── .gemini/INSTALL.md    # agent-executable install steps for Gemini CLI
├── .generic/INSTALL.md   # fallback install steps for any other SKILL.md tool
├── README.md
└── LICENSE
```

## Quick install (one line, in-chat)

Just paste the matching line into your AI coding tool's chat — it will fetch
the instructions and install itself, no manual copying needed:

**Claude Code**
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.claude/INSTALL.md
```

**Codex CLI**
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.codex/INSTALL.md
```

**OpenCode**
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.opencode/INSTALL.md
```

**Cursor**
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.cursor/INSTALL.md
```

**Gemini CLI**
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.gemini/INSTALL.md
```

**Any other tool that supports SKILL.md** (Windsurf, GitHub Copilot CLI, Antigravity, etc.)
```
Fetch and follow instructions from https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/.generic/INSTALL.md
```

That's it — the agent downloads `SKILL.md` and `scripts/new-branch.sh` into
the right place for that tool and confirms once it's active.

## Manual install

If you'd rather do it by hand, or your tool doesn't support fetch-and-follow:

Clone the repo first:
```bash
git clone https://github.com/<your-username>/git-workflow-skill.git
```

Then copy the `git-workflow` folder into your tool's skills directory:

| Tool | Personal / global (all projects) | Project-only |
|---|---|---|
| **Claude Code** | `~/.claude/skills/git-workflow/` | `.claude/skills/git-workflow/` |
| **Codex CLI** | `~/.codex/skills/git-workflow/` | `.codex/skills/git-workflow/` |
| **opencode** | `~/.opencode/skills/git-workflow/` | `.opencode/skills/git-workflow/` |
| **Cursor** | — | `.cursor/skills/git-workflow/` (check current Cursor docs — skill support is newer there) |
| **Gemini CLI** | `~/.gemini/skills/git-workflow/` | `.gemini/skills/git-workflow/` |

Example (Claude Code, global install):
```bash
cp -r git-workflow-skill/git-workflow ~/.claude/skills/git-workflow
```

Example (project-only, so it's shared with anyone who clones your project):
```bash
cp -r git-workflow-skill/git-workflow .claude/skills/git-workflow
```

> Paths above reflect each tool's docs as of mid-2026. These tools are evolving
> fast — if a path doesn't work, check that tool's current skills/plugins
> documentation.

Some tools also support installing straight from a GitHub URL or via a plugin
marketplace command (e.g. Claude Code's `/plugin` system). If your tool has
that, pointing it at this repo works too.

## How to use it after installing

Nothing to configure — just start a new session in your tool and talk normally.
The skill triggers automatically on things like:

- **"commit this"** / **"push this"** → agent checks your current branch; if
  you're on `main`, it creates a properly named feature branch first, then
  commits with a Conventional Commits message.
- **"I'm starting work on the hero section"** → agent creates
  `feature/hero-section` before touching files.
- **"open a PR"** → agent pushes the branch and opens a PR against `main`
  (using `gh pr create` if the GitHub CLI is available).
- **"I'm done, merge it"** → agent walks through review → squash-merge →
  cleanup (delete branch, pull latest `main`).

You can also invoke it explicitly if your tool supports slash-style skill
calls, e.g. in Claude Code: `Use the git-workflow skill to set up this repo`.

If you ever want to do it manually, `scripts/new-branch.sh` is a standalone
script — run `./scripts/new-branch.sh feature/my-thing` from any repo to
safely branch off main.

## The workflow, in short

1. `main` is always clean — never commit to it directly.
2. Branch per feature: `feature/`, `fix/`, `chore/`, `refactor/`, `style/`, `docs/`.
3. Commit with [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `chore:`...).
4. Push the branch, open a PR, review your own diff.
5. Squash-merge into `main`, delete the branch, pull.

Full details, edge cases (merge conflicts, hotfixes, amending commits) and
copy-pasteable commands are in [`SKILL.md`](./SKILL.md).

## Why no `dev`/staging branch?

For solo and freelance-scale projects, `feature → main` is enough overhead —
a `dev` branch layer adds process cost with no payoff until you have multiple
environments or collaborators. See the SKILL.md for when to consider adding one.

## Contributing

PRs welcome — especially install-path corrections as tools update their skills
support, or additional recipes for common git situations.

## License

MIT — use it, fork it, adapt it for your own team's conventions.
