## 
git init


git add . 
git add <filename>
git diff <filename>
git rm <filename>
git mv <filename>
git status
git status -s
git status -l

## show branches
- git branch -l
- git branch -a
- git branch -r
- git branch -M # force create new branch. used during git init process

## branch
- git branch <branch-name>
- git checkout <branch-name>
- git checkout -b <new-branch-name>
- git branch -d <branch-name>
- git branch -d -r <remote-branch-name>
- git branch -c
- git branch -m
- git branch -u or --set-upstream
- git branch --unset-upstream

## handling remotes
- git remote -v
- git remote add <Name> <url>
- git remote add origin <ssh@your-repo-url>
- git remote remove origin

# handling changes
- git restore <filepath>
- git restore --staged <filepath>
- git restore --staged --worktree <filepath> 
- git reset 
- git reset --soft Head~<number> # head moved but files unchanged and indexed
- git reset --hard <commit-id> # head moved, all changes reverted
- git reset --mixed <commit-id> # head moved and files unchanged but un-indexed
- 
