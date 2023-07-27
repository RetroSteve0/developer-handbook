# Resetting Commit History
You can start a new orphan (empty) branch with no commit history to hide all those test messages.

```bash
mozznet@mozznet.com $ git log --oneline origin/main
35def85 (HEAD -> main, origin/main) Implemented LoggedInGuard on root '/' that redirects the user to /main if they have a token session stored in localStorage
a043d1c Merge branch 'main' of github.com:RetroSteve0/mozznet
fc4c2f0 Implemented localStorage for saving token ID securely in browser storage for session persistence
ef52915 Implemented /main. Currently experiencing issues with redirects.
4c8713d Update README.md
244f156 Initial commit using new front end framework
8b3eb8f Merge branch 'main' of github.com:RetroSteve0/mozznet
6845106 Initial commit
ed77888 Initial commit
```

## Create a New Orphan Branch
```bash
git checkout --orphan new_branch_name
```

## Add All Files to the New Branch
```bash
git add .
```

## Make Your Initial Commit
```bash
git commit -m "commit message here"
```

## Delete the Old `main` branch
```bash
git branch -D main
```

## Rename your New Branch to `main`
```bash
git branch -M new_branch_name main
```

## Verify the Commit Log is Empty
```bash
% git log --oneline             
08b2b07 (HEAD -> main, origin/main) Initial commit
```
