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
- staging-area: before git add, the tracked files will appear modified. after git add, indexed files are staged.
- reflog: reference-logs

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
git reset # move file from staging area but changes are still in working tree. so add file again before committing
git reset --soft <commit-id> # roll back to earlier commit but leave changed files as modified in staging area
git reset --soft HEAD~1 # use HEAD~ some number to roll back that many commits
git reset --hard <commit-id> # roll back to earlier commit and change files too 
git reset --mixed <commit-id> # roll back to earlier commit and change index files but not working tree. before commit add files again
```

### Reset vs Restore
- files changed after commit = modified
- modified files are tracked but still need to add to staging-area = file is indexed but unstaged
- git add modified-file to add to staging area = file is in staged 
- git restore file will not restore file if it is already in staged area
  - run git reset on file to get file back to unstaged area first
  - then run git restore on file to revert changes back or run
  - git restore --staged or if you want to change both staged and worktree file, run
  - git restore --staged --worktree
- reset if used alone will just unstage files but reset with --soft/--hard commit-id/head~number will move head


### Remove files
- git rm will remove files from working tree and index
- if you simply delete files, they are removed from working tree but not index
- simple delete means file is deleted and you will see it as deleted in git status

```shell
git rm <filename>
```

### Rename files
- git mv will do following steps
  - make copy of original file and rename it
  - delete original file with old filename

```shell
git mv <original-file> <new-file>
```

## Branching and Merging

### Branch
```shell
git branch <new-branch-name>

# during listing, use --merged or --no-merged to see merged/not-merged branches
git branch -l
git branch -a
git branch -r
git branch -d
git branch -D
git branch -m
git branch -c # copy including reflog and config

git branch -u # --set-upstream; if no branchname passed, take current branch as default
git branch --unset-upstream # if no branchname passed, take current branch as default


```
### checkout
- move head and update working-tree
```shell
git checkout <branchname>
git checkout -b <branchname> <commitID>
```

### Merge
- checkout a new feature branch from existing main
- update changes in new feature branch
- checkout main branch
- run git merge feature-branch-name
```shell
git merge <branchname>
git merge --commit <branchname>
```

### Log

```shell
git log --oneline # current branch
git log --oneline --all # all branches
git log --graph --abbrev-commit --decorate --date=relative --all # shows nice graph with author and relative date
```

### Stash
- stash changes in working tree and index to use later and
- revert back to clean working tree
```shell
git stash list # list entries
git stash show # show stashed changes
```

## Remote Revert Changes
- case1 - only couple of files to revert, modify and push

```shell
# pull latest commit from remote
git checkout earlier-commit-id -- path-to-file
# this will revert only mentioned file to earlier commit
# now change file and commit and push to remote again
```
- case 2 - all files to be reverted back to earlier commit to modify, commit and push
```shell

```