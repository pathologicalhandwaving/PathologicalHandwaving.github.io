---
title: Managing Dotffiles with a Git Bare Repo
date: 2020-05-30
layout: posts
tags:
  - git
  - bare
  - repo
  - dotfiles
---

I have been using a git bare repository to manage my dot files for several years now. There are many great ways to manage and automate dotfiles but I prefer the simplicity of [this method](https://www.atlassian.com/git/tutorials/dotfiles).

``` bash
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc
echo ".cfg" >> .gitignore
cd .cfg
git remote add origin <url>
git remote -v
git add .bashrc
git commit -m "added .bashrc"
git push -u origin master
```



