---
title: Shell Basics & Navigation
date: 2026-08-26
course: CS3620 Operating Systems
tags: [linux-shell, cli]
related:
  - "[[Linux Shell MOC]]"
  - "[[File & Text Commands]]"
  - "[[Executables & Environment]]"
---

# Shell Basics & Navigation

## Table of Contents

- [Intro](#intro)
- [Prompt](#prompt)
- [Paths](#paths)
- [Key Terms](#key-terms)

---

## Intro

> **Cues:** textual vs. graphical interface, CLI, shell

**Notes:**

- Linux has a graphical interface and a textual interface.
- The textual interface — also known as the **Command-Line Interface (CLI)** or terminal — allows full control of the machine and lets you automate tasks.
- In Linux, the **shell** is the program that provides the CLI.

**Summary:** In Linux, the shell is the program that provides the CLI.

---

## Prompt

> **Cues:** prompt format, user_name, machine_name, current_path

**Notes:** Prompt format: `user_name@machine_name:current_path$`

- **user_name** — the name of your user (Linux supports multiple users on the same machine).
- **machine_name** — set when Linux was installed.
- **current_path** — also called the current working directory; all files in Linux are organized in a tree structure.

**Summary:** All files in Linux are organized in a tree structure, and the prompt shows the current working directory within it.

---

## Paths

> **Cues:** absolute path, relative path, `.`, `..`, `~`, cd, ls, pwd

**Notes:**

- **Absolute paths** start with `/`.
- **Relative paths** are relative to the current location: `current_location + relative_path = absolute path`. The current location appears in the prompt (or use `pwd`).
- Shortcuts:
    - `.` → current directory
    - `..` → parent directory
    - `~` → home directory (typically `/home/<user_name>`)
- Commands:
    - `cd` — move from one directory to another
    - `ls` — list the current directory (many options available)
    - `pwd` — print the absolute path of the current directory

**Summary:** `pwd` prints the absolute path of the current working directory.

---

## Key Terms

|Term|Definition|
|---|---|
|**Shell**|The program that provides the CLI in Linux.|
|**CLI (Command-Line Interface)**|The textual interface to Linux; allows full control of the machine and automation of tasks.|
|**Absolute path**|A path that starts with `/`.|
|**Relative path**|A path relative to the current location; `current_location + relative_path = absolute path`.|
