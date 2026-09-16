---
title: File & Text Commands
date: 2026-08-26
course: CS3620 Operating Systems
tags: [linux-shell, cli]
related:
  - "[[Linux-Shell-MOC]]"
  - "[[Shell-Basics-&-Navigation]]"
  - "[[Executables-&-Environment]]"
  - "[[Streams,-Redirection-&-Pipes]]"
---

# File & Text Commands

## Table of Contents

- [Useful Basic Commands](#useful-basic-commands)
- [find](#find)
- [grep](#grep)
- [Key Terms](#key-terms)

---

## Useful Basic Commands

> **Cues:** cp, mv, mkdir, cat, echo, touch, vim/emacs/nano

**Notes:**

- `cp` — copy files/folders (`-r` to copy a directory)
- `mv` — move files/folders
- `mkdir` — create a directory
- `cat` — print a text file
- `echo "something"` — print "something"
- `touch` — create an empty file
- `vim` / `emacs` / `nano` — edit files

**Exercise 1:**

1. Change to your home directory, create a folder named "exercise1".
2. In the new directory, create a directory named "dir1", and two files named "CS3620_1" and "file2".
3. In the "dir1" directory, create two files named "CS3620_2" and "file2".
4. Make a copy of "dir1" named "dir1_copy" in the "exercise1" directory.

**Summary:** `cp -r` copies a directory, `touch` creates an empty file, and `vim`/`emacs`/`nano` are used for editing files.

---

## find

> **Cues:** `find [path] [options]`

**Notes:**

```
find [path] [options]
```

- **Path** — absolute or relative
- **Options** — `-name "xxx"`, `-type f/d`, `-size [+/-]n`, `-mtime n`, `-exec command {} \;`, `-maxdepth levels`, ...
- Reference: [35 Practical Examples of Linux Find Command](https://www.tecmint.com/35-practical-examples-of-linux-find-command/)

**Exercise:** In the exercise1 directory, find all regular files that contain "CS3620" in their file names.

**Summary:** `find` takes a path and options such as `-name`, `-type`, `-size`, `-mtime`, `-exec`, and `-maxdepth`.

---

## grep

> **Cues:** grep, -E, -R, -v, -i, -B/-A/-C, stdin input

**Notes:** Useful to filter text.

- `grep <string> <filename>`
- `-E` — regular expression
- `grep -R <string> <folder>` — recursive search
- `-v` — invert the selection
- `-i` — ignore case
- `-B <n>` / `-A <n>` — show `n` lines of context before/after a match
- `-C <n>` — show `n` lines of context on both sides
- `grep <string>` — process stdin input (see [[Streams,-Redirection-&-Pipes]])

**Exercise:** Use `grep` to write a shell command that accepts input from the keyboard and stores the lines containing "aaa" into a file named "tmp".

**Summary:** `grep` filters text, with `-E` for regex, `-R` for recursive search, `-v` to invert the match, `-i` for case-insensitive matching, and `-B`/`-A`/`-C` for context lines.

---

## Key Terms

|Term|Definition|
|---|---|
|**find**|Searches for files under a path using options like `-name`, `-type`, `-size`, `-mtime`, `-exec`, `-maxdepth`.|
|**grep**|Filters text by pattern; supports regex (`-E`), recursive search (`-R`), inverted match (`-v`), case-insensitive match (`-i`), and context lines (`-B`/`-A`/`-C`).|
