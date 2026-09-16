---
title: Streams, Redirection & Pipes
date: 2026-08-26
course: CS3620 Operating Systems
tags: [linux-shell, cli]
related:
  - "[[Linux-Shell-MOC]]"
  - "[[File-&-Text-Commands]]"
  - "[[Exit-Codes,-Chaining-&-Scripting]]"
---

# Streams, Redirection & Pipes

## Table of Contents

- [Stdin / Stdout / Stderr](#stdin--stdout--stderr)
- [File Redirection](#file-redirection)
- [Pipes](#pipes)
- [xargs](#xargs)
- [Key Terms](#key-terms)

---

## Stdin / Stdout / Stderr

> **Cues:** stdin (fd 0), stdout (fd 1), stderr (fd 2)

**Notes:** Every command-line process has three standard data streams:

- **Standard In (stdin)** — keyboard input by default, file descriptor 0
- **Standard Out (stdout)** — printed to the terminal by default, file descriptor 1
- **Standard Err (stderr)** — printed to the terminal by default, file descriptor 2

**Summary:** Every command-line process has stdin (fd 0), stdout (fd 1), and stderr (fd 2).

---

## File Redirection

> **Cues:** `>` overwrite, `>>` append

**Notes:** You can redirect stdin/stdout/stderr to files using:

- `>` (overwrite)
- `>>` (append)

Examples:

- `ls > /tmp/file1` — redirect stdout into a file
- `ls 2> /tmp/file2` — redirect stderr into a file
- `strace ls 2>&1` — redirect stderr into stdout
- `strace ls 2>/tmp/syscalls.log`
- `echo "file content" > /tmp/newfile`

**Exercise 3:**

1. In the "exercise1" folder, append "uiowa" to the end of "file2" using `echo` and file redirection.
2. Copy "file2" to a new file "file1" without using the `cp` command.

**Summary:** `>` overwrites a file while `>>` appends to it, and stdout/stderr can be redirected independently (e.g., `2>` for stderr).

---

## Pipes

> **Cues:** `|`, connecting stdout to stdin

**Notes:** Commands like `grep` (see [[File-&-Text-Commands]]) are typically used with **pipes**: `|`

- `<command1> | <command2>` connects the stdout of command1 to the stdin of command2.

**Exercise:** Use `grep` and a pipe to accept input from the keyboard and store the lines containing "aaa" but not "bbb" into a file named "tmp".

**Summary:** A pipe (`|`) connects the stdout of one command to the stdin of the next.

---

## xargs

> **Cues:** xargs, -I{}, -n1 -P1

**Notes:** Useful for applying the same command to a list of strings.

```
ls -1 | grep -v secret | xargs -n1 -P1 -I{} cp "{}" "{}_copy"
```

- `xargs -I{} [command]`
- `ls -1` — list files, one per line
- `grep -v secret` — remove lines containing "secret"
- `xargs` options: `-n1 -P1` passes the content of each line in the input to a new process; `-I{}` substitutes `{}` with the content of the processed line.
- Reference: [xargs Examples](https://www.thegeekstuff.com/2013/12/xargs-examples/)

**Exercise:** In the "exercise1" folder, copy every file that contains "CS3620" in the name to a new file named "{originalname}_copy".

**Summary:** `xargs -I{}` substitutes `{}` with each line of input, applying the same command to a list of strings.

---

## Key Terms

|Term|Definition|
|---|---|
|**stdin / stdout / stderr**|The three standard data streams of a command-line process (file descriptors 0, 1, 2).|
|**Pipe (`\|`)**|Connects the stdout of one command to the stdin of another.|
