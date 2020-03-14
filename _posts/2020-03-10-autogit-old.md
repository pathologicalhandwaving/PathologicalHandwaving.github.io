---
title: AutoGit.sh
layout: posts
category: Scripts
tags: scripts, bash, git, automation
---

The following script `autogit.sh` works currently from your current project directory. 

  - *TODO:* Add watcher

The script checks your connection, git config settings, and authorization then executes a pull, clean, commit, and push.
 
``` bash
#!/bin/bash
# autogit.sh
# Automatically pull, add changed, commit with file name, and push to remote
# PathologicalHandwaving
# Why is this a script not an alias? Because its a module.

# Check Connection
ssh-add -l &>/dev/null
#[[ "$?" == 2]] && eval $("ssh-agent") > /dev/null

# Check Git Config
if [ ! $(git config user.name) ]
then
    git config --global user.name <username>
    git config --global user.email <email>
fi

# Check Auth
ssh-add ~/.ssh/github
[[ "$?" == 1 ]] && expect $HOME/.ssh/ > /dev/null

# Pull
git pull

# Clean and Push
REMOTE=$(git remote get-url origin)
URL=git@github.com:${REMOTE##*github.com/}
[[ $REMOTE == "http"* ]] && git remote set-url origin $URL

git add --all
git commit -am "File Modified: $*. AutoGit commit on change away!"
git status
git push origin $(git rev-parse --abbrev-ref HEAD) --force

echo "All Done!" | toilet --filter="border" --gay -t

exit 0
```
