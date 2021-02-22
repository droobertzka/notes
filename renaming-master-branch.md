# A Guide to Renaming Master Branches in Git

The term _master_ by definition references slavery, a tragic human atrocity that should not be used carelessly in unrelated contexts such as relationships in tech tooling. See the [Software Freedom Conservancy statement](https://sfconservancy.org/news/2020/jun/23/gitbranchname/). The following is a guide on changing existing git repos over from _master_ to _main_.

**OVERVIEW** 
One dev updates their local and remote, then teammates' correct their local clones of the repo, be sure to lock down the new "main" branch, and update your global git config as in approach 2.

## Your Local & Remote
```sh
# 1. Rename your local branch.
git branch -m master main

# 2. Push renamed branch upstream and set remote tracking branch.
git push -u origin main

# 3. Log into host (GitHub, GitLab, Bitbucket, etc.), change the "default branch", update master permissions/restrictions.
# 4. Add permissions/restrictions to main.

# 5. Delete the old branch upstream.
git push origin --delete master

# 6. Update the upstream remote's HEAD. 
git remote set-head origin -a
```

## Teammates' Local Clones
```sh
# 1. Switch to the "master" branch:
git checkout master

# 2. Rename it to "main":
git branch -m master main

# 3. Get the latest commits (and branches!) from the remote:
git fetch

# 4. Remove the existing tracking connection with "origin/master":
git branch --unset-upstream

# 5. Create a new tracking connection with the new "origin/main" branch:
git branch -u origin/main
```

## Everyone
Create an alias in your global .gitconfig to make `main` the default branch name for new repos. You can't override `git init`, so create a `git new` command instead.
```sh
git config --global alias.new '!git init && git symbolic-ref HEAD refs/heads/main'
```
