# Install git-workflow skill (any SKILL.md-compatible tool)

You are an AI coding agent, not necessarily Claude Code, Codex, Cursor,
Gemini CLI, or OpenCode. Follow these steps yourself, right now, in order.
Do not just describe them to the user — execute them.

## 1. Figure out where this tool looks for skills

Most current AI coding tools that support the open SKILL.md standard look for
skills in one of these patterns — check your own tool's docs, config, or
existing directory structure to find which applies here:
- `.<toolname>/skills/<skill-name>/SKILL.md` (project-level)
- `~/.<toolname>/skills/<skill-name>/SKILL.md` (personal/global)
- `~/.config/<toolname>/skills/<skill-name>/SKILL.md`

If you can't determine this confidently, ask the user: "Where does
[this tool] look for skill/plugin files?" rather than guessing and creating
a folder the tool won't actually read.

## 2. Create the target directory and download the skill files

Once you know `<TARGET>`:

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
- Where the skill was installed, and which tool-specific convention you used.
- One-line summary: it makes sure they never commit directly to `main` —
  every commit goes through a `feature/`/`fix/`/`chore/` branch with a
  Conventional Commits message, then a PR and squash-merge.
- They can test it by saying "commit this" and confirming you check the
  current branch before committing.

Do not print the full SKILL.md contents back to the user unless they ask —
just confirm installation succeeded.
