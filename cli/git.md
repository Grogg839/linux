# Git Quick Reference

## How it works
```
working files ──add──▶ staging ──commit──▶ history ──push──▶ GitHub
                                                   ◀──pull──
```
- **Commit** = snapshot of the project.
- **Branch** = label pointing at a commit.
- **origin** = the GitHub copy.

## Key concepts

**Staging:** `add` puts changes in the box and `commit` seals it. This lets you commit related changes together, e.g. the bug fix now and the new feature separately.

**Branches:** a branch is a sticky note on a commit, not a copy of your files. When you commit, the note moves forward.
```
A ← B ← C ← D ← E      git switch -c exp, then commit twice
            main  exp  → only `exp` moves; switching branches swaps your files
```

**HEAD:** "you are here", i.e. the branch you're on. `HEAD~1` means one commit back.

**Merging:**
- If `main` hasn't moved since you branched, the merge is a **fast-forward**: the note just slides forward.
- If both branches moved, Git makes a merge commit with two parents.
- A **conflict** only happens when both branches changed the same lines.
```
        ┌─ E ← F ─┐
A ← B ← D          M   main
        └─ G ──────┘
```

**`main` vs `origin/main`:** `origin/main` is where GitHub's main was the last time you checked. `fetch` updates it; `pull` = `fetch` + merge. "Ahead by 2" means you have 2 commits GitHub doesn't.

**Reset vs revert:**
- `reset` moves the note back, which **rewrites** history.
- `revert` adds an undo commit.
- Not pushed yet → reset is fine. Already pushed → use revert.

**Rebase:** replays your commits on top of main to give a straight history. It rewrites history, so never rebase pushed commits. Stick to merge for now.

## Setup (once)
```bash
git config --global user.name "Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

## Start
```bash
git init                         # new repo
git clone git@github.com:u/r.git # copy existing
git remote add origin <url>      # link to GitHub
git push -u origin main          # first push
```

## Daily
```bash
git status
git add .            # or a specific file
git commit -m "Add thing"
git push
git pull
```

## Branches
```bash
git switch -c feature   # new branch
git switch main         # change branch
git merge feature       # merge into current
git branch -d feature   # delete
```
**Conflict:** edit the file, remove the `<<<` `===` `>>>` markers, then `git add` and `git commit`.

## History
```bash
git log --oneline --graph --all
git diff
```

## Undo
| Want to | Command |
|---|---|
| Discard file edits | `git restore file` |
| Unstage | `git restore --staged file` |
| Fix last commit | `git commit --amend` |
| Undo last commit (keep changes) | `git reset HEAD~1` |
| Undo a pushed commit | `git revert <id>` |
| Park work | `git stash` / `git stash pop` |

## .gitignore
```
__pycache__/
.venv/
.env
result
```
