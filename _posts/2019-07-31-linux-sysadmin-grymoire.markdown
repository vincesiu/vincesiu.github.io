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

### tar

```
# Serialize to tar format
tar -cvf <archive>.tar <directory>
# Serialize to tar and then compress with gzip
tar -zcvf <archive>.tar.gz> <directory>
```

### vmstat

```
vmstat 1 # prints report every second
vmstat -d 1 # prints report on disk stats, so new columns
```

Most useful columns imo are:
* Procs:r/b
    + r: runqueue, either running or waiting to run
    + b: this is number of processes in uninterruptible sleep
* IO:bi/bo
    + this is the number of memory swapped in and out /s
* Memory:free
    + amount of idle memory

## memory management

ncdu 

## jq

example.json
```
{
	"meow" : "nyan",
	"woof" : [
	{ "color" : "red" },
	{ "color" : "blue" },
	{ "color" : "green" }
	       ],
}
```

basic jq usage
```
cat example.json | jq '.'
jq '.' example.json
```

getting a key
```
jq '.meow'
jw '.[meow]'
```

listing all keys of an object
```
jq 'keys' example.json
```

length of an object
```
jq '.woof | length'
```

getting a key from every element in an array
```
jq '.woof[] | .color'
```

### Aggregation and Composition

piping
```
jq '.woof[] | .color'
```

getting multiple keys

```
jq '.meow,.woof'
```
