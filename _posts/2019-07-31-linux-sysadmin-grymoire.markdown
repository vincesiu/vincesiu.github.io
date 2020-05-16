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

## windows vs dos line endings

- dos2unix is your command
- `cat -v ${file} | grep ^M`
  * this command will find any of the CRLF line endings in your file

## git 

- `git branch -a`
- `git reset ...`
- `git log --oneline --graph --decorate --all`

### diff goodness
- `git diff --cached`
  * shows the difference between index and current commit
- `git diff`
  * shows the difference between index and working directory
- `git diff HEAD`
  * shows the difference between current commit and working directory

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
	       ]
}
```

### basic jq usage

Print the whole struct

```
cat example.json | jq '.'
jq '.' example.json
```

Getting a key
```
jq '.meow'
jw '.[meow]'
```

listing all keys of an object
```
jq '. | keys' example.json
```

length of an object
```
jq '.woof | length'
```

getting a key from every element in an array
```
jq '.woof[] | .color'
```

### Explanation of Piping and Iteration

From my understanding, piping is used to separate function calls and field accesses. Looping and iteration are also usually using pipes.
'.' is the input value at each stage of a pipeline, so as an example:

```
jq '.woof[].color'
jq '.woof | .[] | .color'
jq '.woof | .color' # does not work because the .color filter is trying to access the color field of an array, which doesn't make sense
```

getting multiple keys
```
jq '.meow,.woof'
```

### Outputting csv and maps

csv takes arrays
maps will apply the function to all the elements in an array if a single array is passed, or all the elements if multiple elements are passed. Feels suspiciously like the Python list function
```
jq -r '.woof | map(.color) | @csv'

```

Anything more complicated? PLEASE USE A REAL PROGRAMMING LANGUAGE


## find

```
# find and delete by inum
find . -type f -inum ${INUM} -delete

# find and delete by inum by another way
find . -type f -inum ${INUM} -exec rm {} \;

# find by case insensitive name
find . -iname '*.jpg'

# list everything
find .
```

## xargs

input.txt
```
123
456
789
```

```
# equivalent of running echo 123 456 789
$ cat input.txt | xargs echo
123 456 789

# equivalent of running echo 3 times for each line
$ cat input.txt | xargs -I {} echo
123
456
789

# running xargs in parallel
$ cat input.txt | xargs -P 10 -I {} echo
123
456
789
```
