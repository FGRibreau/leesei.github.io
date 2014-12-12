title: Git note
toc: true
date: 2014-12-11 17:34:15
tags:
- git
- shell-tool
---

http://ndpsoftware.com/git-cheatsheet.html

## Merging from forked repo

https://www.openshift.com/wiki/github-workflow-for-submitting-pull-requests

https://help.github.com/articles/syncing-a-fork

```bash
# setup fork origin as upstream
git remote add upstream <fork origin url>

# pull the latest changes from upstream
git fetch upstream
git fetch upstream --tags

# assuming you are on <feature> branch and have uncommited updates
git stash
git co master

# merge the latest changes to current repo's master
git merge upstream/master

# push the updates changes to our fork
git push origin master
git push origin --tags

# rebase <feature> branch onto latest code from master (expect conflicts)
# can also used before submitting pull request/push to repo
git co <feature>
git rebase master

# apply uncommitted changes
git stash pop
```

## Deleting branch

```bash
# delete remote branch
git push origin :<branch>

# delete remote branch with dash
git push origin :refs/heads/<branch-with-dash>

# delete local branch
git branch -d <branch>

# delete local branch (force)
git branch -d <branch>
```

## Set tracking branch

```bash
git branch --set-upstream feature_branch origin/origin_branch
```

## gitweb

```bash
# start server
git instaweb -d webrick --start

# visit http://localhost:1234

# stop server
git instaweb -d webrick --stop
```

## Get current branch in shell

```bash
parse_git_branch(){
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/[\1]/';
}
```

## create repo archive

```bash
git archive master -o <repo>.<tag>.zip
```

## submodules

### using project with submodules

```bash
# clone project with submodules
git submodule init
git submodule sync
git submodule update
git submodule status
```

## Old notes 

```bash
git checkout -b redesign

# update working branch
git pull origin
git merge master
# OR
? git pull origin master:redesign

# commit
git pull origin
git checkout master
git merge redesign
git push origin master:master
# OR 
git checkout redesign
git rebase master
git push origin redesign:master

# delete local branch
git branch -d redesign # after merge
git branch -D redesign # force

# delete remote branch
git push origin :redesign

# delete whole tree
git push origin :master

# update a commit (unpushed)
git commit --amend <file>

# show commit info
git log [<some/path>]
git show [<some commit id>]
```