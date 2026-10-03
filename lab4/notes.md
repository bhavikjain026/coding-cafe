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

**Q9. What are the four steps of the loop you just did twice?**
1. Edit (change or create files in the working directory). 2. Check with `git status`. 3. Stage with `git add`. 4. Commit with `git commit -m "message"` (and check `git log`).

**Q10. Why does README.md get a special name and a special place?**
`README.md` in the top folder is the conventional "start here" file: GitHub automatically displays it on the repository's front page, and anyone opening the project knows to read it first. A file called `notes.md` buried in a folder wouldn't be found or shown automatically.

**Q11. What did `gh auth login` do that means you won't be asked for a password when you push?**
It logged me in to GitHub through the browser and saved an access token on my laptop, then set itself up as Git's credential helper. When I push, Git asks `gh` for that token instead of asking me for a password (GitHub no longer accepts account passwords for Git anyway).

**Q12. What is showing on the repository's front page, and why that file?**
The file list and, below it, my `README.md` rendered as formatted text (heading, bold name and roll number, bullet list). GitHub automatically renders the README in the top folder because it's meant to describe the project to visitors.

**Q13. Did pushing change your local history in any way?**
No. `git log --oneline` shows the same commits with the same hashes. Pushing only copies commits to GitHub; the only local change is that Git now records `origin/main` as tracking my `main` branch.

**Q14. Difference between a private repository and a repository not existing on GitHub at all?**
A private repository exists on GitHub with a full copy of my history, but only I and the collaborators I invite (the TAs) can see it. If it didn't exist on GitHub, the code would only be on my laptop, so nobody else could ever access it and there'd be no backup.
