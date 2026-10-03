# Lab 4 — Git & GitHub: Notes

**Q1. What did `--global` mean? What if you left it out?**
`--global` saves the setting in my user-wide config file (`~/.gitconfig`), so it applies to every repository on this laptop. Without it, Git writes to the current repository's own `.git/config`, so the setting only applies to that one repo (and fails if you're not inside a repo).

**Q2. What appeared in `ls -a` but not in `ls`? What is inside it?**
A hidden `.git` folder (hidden because its name starts with a dot). It is the repository itself: Git's database of commits and file snapshots (`objects/`), branches and tags (`refs/`), `HEAD`, and the repo's `config`.

**Q3. Roughly how many files/folders is Git offering to track? Anything you didn't write?**
Only three entries: `.DS_Store`, `README.md` and `week02/`. `.DS_Store` is a hidden file macOS creates on its own, not something I wrote. `.venv/` didn't show up because Python's venv puts its own `.gitignore` containing `*` inside it, and the empty `week01/` didn't show because Git doesn't track empty folders.

**Q4. Compare this `git status` with the one from Q3. What disappeared?**
`.DS_Store` disappeared from the untracked list because `.gitignore` now tells Git to ignore it. `.gitignore` itself appeared as a new untracked file.

**Q5. Should `.gitignore` be committed, or ignored too? Why?**
It should be committed. It's part of the project's setup: anyone who clones the repo (or me on another laptop) gets the same ignore rules, so junk like `.venv/` and `.DS_Store` never gets committed by accident.

**Q6. README.md moved between which two headings? What happened in the three-places model?**
It moved from "Untracked files" to "Changes to be committed". It went from the working directory into the staging area (index), ready to go into the next commit in the repository.

**Q7. What did Git print after the commit? How many files changed?**
It printed the branch and short hash with the message, `[main (root-commit) 628fe4e] Lab work so far`, then `5 files changed, 1446 insertions(+)` and a `create mode 100644` line for each new file (`.gitignore`, `README.md` and the three files in `week02/`).

**Q8. What are the first seven characters of a commit called, and what are they for?**
They are the short commit hash (an abbreviated SHA-1 hash, e.g. `628fe4e`). The hash is a unique ID for that commit, so you can refer to it in commands like `git show 628fe4e` or to go back to that version.
