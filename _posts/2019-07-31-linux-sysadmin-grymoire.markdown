---
layout: post
title:  "Linux Sysadmin Grymoire"
date:   2019-07-31 11:35:51 +0000
categories: linux sysadmin grymoire
---

# Linux Sysadmin Grymoire

Random tidbits that I need to reference every now and then

---

## bash

### rewrite previous command

- helps you edit the current command in an editor
    * `ctrl-x ctrl-e`

## git 

- `git branch -a`
- `git reset ...`
- `git log --oneline --graph --decorate --all`

### regular workflow

1. `git pull`
2. `git rebase --onto origin/master`

## networking

### iptables

- `iptables-restore {iptables_file}` restore iptables from this file
- `iptables -L` lists iptable rules
- `iptables -F` drops all the iptables

## process management

### htop

### ps

## memory management

ncdu 
