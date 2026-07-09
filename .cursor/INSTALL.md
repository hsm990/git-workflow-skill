# Install git-workflow skill (Cursor)

You are an AI coding agent. Follow these steps yourself, right now, in order.
Do not just describe them to the user — execute them.

## 1. Determine install scope

If you're already working inside a specific project the user wants this
scoped to, install as **project** scope. Otherwise, ask the user in one short
message: "Install git-workflow for all your projects, or just this one?"
Default to **project** scope if ambiguous — Cursor's skill support is newer
and project-level is the safer default.

- Personal (all projects, if supported by this Cursor version): target =
  `~/.cursor/skills/git-workflow`
- Project (this repo only): target = `.cursor/skills/git-workflow`

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

## 3. If Cursor doesn't auto-discover this path

Cursor's skill/rules support has changed across versions. If plain
`.cursor/skills/` doesn't get picked up, check whether this version of Cursor
instead expects:
- A `.cursor/rules/` directory with an `.mdc` file, or
- Registration via a marketplace/plugin command (e.g. `/add-plugin`)

If so, tell the user what you found and ask whether they want you to convert
`SKILL.md`'s content into that format instead (same instructions, different
wrapper — the workflow rules themselves don't change).

## 4. Verify

```bash
ls <TARGET>
```
You should see `SKILL.md` and `scripts/new-branch.sh`.

## 5. Confirm to the user

Tell the user, briefly:
- The skill is installed at `<TARGET>` (or note if you had to adapt the format).
- One-line summary: it makes sure they never commit directly to `main` —
  every commit goes through a `feature/`/`fix/`/`chore/` branch with a
  Conventional Commits message, then a PR and squash-merge.
- They can test it by saying "commit this" and confirming you check the
  current branch before committing.

Do not print the full SKILL.md contents back to the user unless they ask —
just confirm installation succeeded.
