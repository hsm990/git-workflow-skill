# Install git-workflow skill (Claude Code)

You are an AI coding agent. Follow these steps yourself, right now, in order.
Do not just describe them to the user — execute them.

## 1. Determine install scope

If you're already working inside a specific project the user wants this
scoped to, install as **project** scope. Otherwise, ask the user in one short
message: "Install git-workflow for all your projects, or just this one?"
Default to **personal** scope if the context makes this ambiguous and you
can't ask.

- Personal (all projects): target = `~/.claude/skills/git-workflow`
- Project (this repo only): target = `.claude/skills/git-workflow`

## 2. Create the target directory and download the skill files

Replace `<TARGET>` with the path chosen above.

```bash
mkdir -p <TARGET>/scripts
curl -sL https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/SKILL.md -o <TARGET>/SKILL.md
curl -sL https://raw.githubusercontent.com/hsm990/git-workflow-skill/main/scripts/new-branch.sh -o <TARGET>/scripts/new-branch.sh
chmod +x <TARGET>/scripts/new-branch.sh
```

If `curl` isn't available, use `wget -O` instead, or clone the whole repo and
copy the `git-workflow` folder into `<TARGET>`'s parent directory:

```bash
git clone https://github.com/hsm990/git-workflow-skill.git /tmp/git-workflow-skill
cp -r /tmp/git-workflow-skill/git-workflow/. <TARGET>/
rm -rf /tmp/git-workflow-skill
```

## 3. Verify

```bash
ls <TARGET>
```
You should see `SKILL.md` and `scripts/new-branch.sh`.

## 4. Confirm to the user

Tell the user, briefly:
- The skill is installed at `<TARGET>`.
- It's active starting now (or next session, if this tool requires a restart
  to pick up new skills — check and say which applies).
- One-line summary: it makes sure they never commit directly to `main` —
  every commit goes through a `feature/`/`fix/`/`chore/` branch with a
  Conventional Commits message, then a PR and squash-merge.
- They can test it immediately by saying something like "commit this" and
  confirming you check the current branch before committing.

Do not print the full SKILL.md contents back to the user unless they ask —
just confirm installation succeeded.
