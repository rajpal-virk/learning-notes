# Git Notes


## Introduction

---

<br>

## Keywords

---

- repo: repository (working directory)
- local branch: these are in your local repo
- remote branch: these are in your remote repo
- PR: pull request - to merge changes from a branch to main
- push: pushing changes directly to remote branch from local branch
- head: pointer that determines the branch or commits that last checked out
- working tree: current working directory
- index: git staging area where user commits new changes


<br>

## Best Practices

- create repo names in lowercases and replace space between words with hyphen(-)
- create a main branch but enable protection for it
- always work in dev or other pre-prod branches
- make a final pull request once product is ready
- ensure the pull request has a proper tag
- all commit messages should be logical and can include issue no.
- don't need to push every single commit to GitHub, do it after few commits

<br>

## Initializing

---
 You have 2 options:

### 1. Create a project 
- From local repo to existing remote (GitHub) repo
```shell
cd <working-dir-path>
git init # initialize git (Note: use can use -b flag to also create local branch)
git branch -M main # create a local branch 
git remote add origin <ssh@your-remote-repo> # add a remote repo's default branch
git pull origin main # pull all files from remote first before pushing local changes/files
git checkout -b dev # at this point you can checkout main branch to dev branch so main stays unchanged
git add .
git commit -m 'First  commit'
git push -u origin dev # this will create a new remote branch and start tracking it in git
```

### 2. Get a Project
- From existing remote (GitHub) repo to local repo
```shell
cd <parent-directory-path> # parent directory > GitHub repo folder
git clone <ssh@your-remote-repo>
```

<br>

## Snapshotting

---

### Adding Files
```shell
git add <filename> # add specific file
git add . # add all files of current working folder
```

### Status of files
```shell
git status
git status -s # --short
git status -b -s # -b flag is to show branch 
```
- '' = unmodified
- M = modified
- T = file type changed
- A = added
- D = deleted
- R = renamed
- C = copied
- U = updated but unmerged


### Difference b/w files/commits
```shell
git diff <filename1> <filename2>
git diff <commit1> <commit2>
```


### Restore
- Restore working tree files
- Revert all changes in working tree after commit
```shell
# if you made some changes to a tracked file, which make file to appear
# modified in git status (since you have not committed this file), 
# you can undo all those changes with git restore
git restore <filename> # restore file from index

# you made changes and committed changes. 
# now you made some changes to file again after commit but you wish to revert files back to 
# last committed stage 
# --staged flag restores only index file, which does note make sense, since if the file is still
# modified, it continues to appear in staging area
git restore --staged <filename> # restore indexed file from Head

## --worktree and --staged together is best to restore files in both working-tree and staging-area
git restore --staged --worktree <filename> # restore both indexed file and working-tree file
```


### Reset
- rolling back project to earlier commit
- deletes commits after the roll-back commit point
- if you push to remote then you might see conflicts since remote has earlier commits but local does not.
```shell
git reset --soft <commit-id> # roll back to earlier commit but leave changed files as modified in staging area
git reset --hard <commit-id> # roll back to earlier commit and change files too 
```



### Log

```shell
git log --graph --abbrev-commit --decorate --date=relative --all # shows nice graph with author and relative date

```