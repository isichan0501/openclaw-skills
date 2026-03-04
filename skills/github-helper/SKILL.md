---
name: github-helper
description: Work with GitHub repos, issues, and pull requests using the gh CLI and git. Use when the user asks to create or update GitHub Issues/PRs, draft release notes, manage labels/milestones, review diffs, prepare branches, or automate common GitHub workflows.
metadata: {"openclaw":{"requires":{"bins":["gh","git"]},"homepage":"https://github.com/cli/cli"}}
---

# GitHub Helper

Use this skill to reliably perform common GitHub workflows via **git** + **gh**.

## Quick start (always)

1. Confirm you are in the target repo.
2. Ensure `gh auth status` is logged in to the right account.
3. Prefer small, reviewable changes and include links/ids in outputs.

## Task playbook

### 1) Repo sanity

Run:

```bash
pwd
git status
git remote -v
gh auth status
```

If the user gave a repo URL, clone it and `cd` into it.

### 2) Issues

Common:

```bash
# list
gh issue list --limit 50

# create
gh issue create --title "..." --body "..." --label "bug" --assignee "@me"

# view
gh issue view <number> --web
```

### 3) Branch + commit

```bash
git checkout -b <branch>
# edit files
git add -A
git commit -m "<message>"
```

### 4) Pull requests

```bash
# push current branch
git push -u origin HEAD

# create PR
gh pr create --fill

# view/check
gh pr view --web
gh pr checks
```

For review: summarize the diff and call out risk areas.

### 5) Release notes (lightweight)

If asked to draft release notes, prefer:

```bash
gh pr list --state merged --limit 50 --base main
```

Then group by feature/fix/chore and include PR links.

## Repo-local conventions

If `{baseDir}/references/conventions.md` exists, read it and follow it.

## Resources

- `references/conventions.md`: optional repo conventions (branch naming, labels, PR template hints)
- `scripts/`: optional automation helpers (create issue/PR templates, bulk label ops)
