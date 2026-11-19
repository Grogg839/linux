# Linux From Scratch: Learning Guide

## The bare minimum: 8 topics

| # | Topic | What to actually know | You've got it when you can… |
|---|---|---|---|
| 01 | **Filesystem** | Everything is a file. What `/etc`, `/home`, `/var`, `/tmp` and `/proc` are for, plus why NixOS adds `/nix/store`. Absolute vs relative paths, `~`, hidden dotfiles | Explain where config, logs and user data live without looking it up |
| 02 | **Shell basics** | Command + flags + arguments, `man` and `--help`, `ls cd cp mv rm mkdir cat less`, globbing (`*.md`) | Move around and reorganise files using only the terminal |
| 03 | **Pipes & redirection** | stdin, stdout and stderr, `\|`, `>`, `>>`, `2>&1`, exit codes, `&&` / `\|\|`, plus `grep`, `find`, `wc`, `sort` | Answer a question like "which 5 files in /etc are biggest?" in one line |
| 04 | **Users & permissions** | Reading `ls -l`, rwx and octal (`chmod 644`), owners and groups, `sudo`, why root is dangerous | Explain why a script won't run and fix it |
| 05 | **Processes** | `ps`, `top`/`htop`, PIDs, signals (`kill`, what Ctrl-C actually sends), jobs (`&`, `fg`, `bg`) | Find and kill a runaway process |
| 06 | **Environment** | Env vars, `PATH`, `which`, what your shell reads at startup | Explain how typing `vim` finds the binary |
| 07 | **Packages, the Nix way** | `nix-shell -p` for trying things, `configuration.nix`, `nixos-rebuild switch`, generations and rollback | Add a package declaratively, break something, then roll back |
| 08 | **Services, logs & networking** | `systemctl status`, `journalctl -u`, `ip a`, `ping`, `ss -tlnp`, `ssh` + keys, `rsync` | SSH into the ThinkCentre with a key and read a service's logs |

That's the whole list. Everything else (shell scripting, cron and timers, disks, firewalls) builds on these. Topic 08 leads straight into the home server, so that's the capstone.

## Repo structure

Keep it lean so maintaining it never feels like a chore:

```
~/Code/linux/
├── README.md          # the 8-topic checklist + links to notes
├── notes/
│   ├── 01-filesystem.md
│   ├── 02-shell-basics.md
│   └── ...            # create each only when you start that topic
├── scripts/           # anything you wrote that actually runs
└── LOG.md             # dated one-liners: what you did, what confused you
```

## Note template

Use the same template for every note:

```markdown
# Topic name

## In my own words
(Explain it like you're teaching a friend. No copy-paste.)

## Commands I actually ran
(Command, a trimmed bit of real output, and what it told you.)

## What broke / surprised me
(The most valuable section. Errors and how you fixed them.)

## Still don't get
(Open questions. Delete them as you answer them.)
```

## The learning loop (one session = one loop)

1. **Read a little.** The `man` page plus one chapter of *The Linux Command Line* by William Shotts (free online) is enough. `nix-shell -p tldr` gives quick examples.
2. **Do it.** Run the commands and deliberately break things. You can't break much in WSL, and NixOS rollback covers you on the server.
3. **Write it from memory, then check.** Fill the note without looking, then correct it. The correcting is where it sticks.
4. **Commit with a message that states what you learned**, e.g. `git commit -m "permissions: execute bit is needed to cd into a dir"`. The `git log` then doubles as a revision sheet.
5. **Tick it off in the README** only once you can do the "you've got it when…" task cold.

## Two rules

- Nothing goes in a note that you haven't run yourself.
- The "What broke / surprised me" section is never empty.

Notes written that way are worth rereading; copied tutorials aren't.
