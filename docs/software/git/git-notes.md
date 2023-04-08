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
1. From local repo to existing remote (GitHub) repo
```shell
cd <working-dir-path>
git init
git branch -M main
git remote add origin <ssh@your-remote-repo>
git pull origin main
git checkout -b dev # at this point you can checkout main branch to dev branch so main stays unchanged
git add .
git commit -m 'First  commit'
git push -u origin dev
```
2. From existing remote (GitHub) repo to local repo
```shell
cd <parent-directory-path>
git clone <ssh@your-remote-repo>
```

<br>

##