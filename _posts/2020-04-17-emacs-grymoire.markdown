---
layout: post
title:  "Emacs Grymoire"
date:   2020-04-17 10:43:51 +0000
categories: emacs grymoire
---

# Emacs Grymoire

Random tidbits that I need to reference every now and then. Everything is assumed emacs 26.1

# Help / Documentation

* Where are the manuals?
  - C-h r
* Provide documentation for a function
  - C-h f ${FUNCTION}
* Search for commands 
  - C-h a ${KEYWORD} ...

# Elisp

todo

# Movement / Editing Commands

* Undo: 
  - C-_
  - C-x u
* Go to line
  - M-g M-g ${LINENUM}


# Emacs CLI Options

* Start without using emacs .emacs files
  - emacs -q

# Emacs daemon mode

* cli start with daemon
  - emacs --daemon
* command to exit out of emacs
  - M-x save-buffers-kill-emacs
* cli start with debug mode one
  - emacs --debug-init
