---
title: Executables & Environment
date: 2026-08-26
course: CS3620 Operating Systems
tags: [linux-shell, bash-scripting, permissions]
related:
  - "[[Linux-Shell-MOC]]"
  - "[[Shell-Basics-&-Navigation]]"
  - "[[File-&-Text-Commands]]"
  - "[[Exit-Codes,-Chaining-&-Scripting]]"
---

# Executables & Environment

## Table of Contents

- [Two Types of Commands](#two-types-of-commands)
- [Executables](#executables)
- [Environment Variables](#environment-variables)
- [Sudo](#sudo)
- [Suggested Packages](#suggested-packages)
- [Key Terms](#key-terms)

---

## Two Types of Commands

> **Cues:** built-ins, executable programs

**Notes:**

- **Built-ins** (e.g., `cd`) — part of the shell itself.
- **Executable programs stored on disk** (e.g., `pwd`, `ls`) — found via `PATH`; `which` shows the location.

**Summary:** Commands are either shell built-ins (like `cd`) or executable programs stored on disk (like `pwd`, `ls`).

---

## Executables

> **Cues:** running an executable, `./`, chmod +x

**Notes:**

- Run an executable with: `<executable> <arg1> <arg2> <arg3> <...>` (arguments separated by spaces).
- `<executable>` is an absolute or relative path.
- If the executable is in the current directory, use `./<executable>`.
- The file needs to be executable; check with `ls -la` (look for `-rwx------`).
- Set executable permission with `chmod +x <file>`.

**Exercise:** Copy the `ls` program into your home directory, remove the executable permission, and then try to run it in your home directory.

**Summary:** Executable permission is checked with `ls -la` and set with `chmod +x <file>`.

---

## Environment Variables

> **Cues:** env, PATH, export, ~/.bashrc, which

**Notes:**

- Programs can access environment variables; check with `env`.
- The **`PATH`** variable stores the default directories where the shell looks for executables.
- `which <command>` shows the location of an executable found via `PATH`.
- Set with `export VAR="value"` — this is only valid "per-shell".
- To define a variable every time the shell is launched, modify `~/.bashrc`.

**Exercise 2:**

1. Create a directory named "exercise2" in your home directory.
2. Copy the `pwd` command into the exercise2 directory.
3. Remove the executable permission from the copied `pwd`.
4. Add `~/exercise2` to the beginning of your `PATH` (using `export`).
5. Try running the `pwd` command — what happens and why?

**Summary:** Modifying `~/.bashrc` is how you define an environment variable every time the shell is launched.

---

## Sudo

> **Cues:** sudo, root user, sudoer, groups

**Notes:**

- Some commands require more privileges than the standard user.
- Use `sudo <command>` to execute a command as the root user (requires your user's password).
- Examples: `sudo apt install <package>`, `sudo apt purge <package>`.
- Only users in the sudoer list can execute commands as root; check with `groups`.

**Summary:** Only users in the sudoer list can use `sudo`, which can be checked with the `groups` command.

---

## Suggested Packages

> **Cues:** apt update, apt upgrade, apt install (dev tools)

**Notes:** On your virtual machine:

1. Refresh the APT package manager's package index: `sudo apt update`
2. Download and install newer versions of packages on your system: `sudo apt upgrade`
3. Install essential development tools: `sudo apt install git openjdk-8-jdk vim build-essential ssh gdb make`

By default, the first user created during Ubuntu installation is in the sudo group.

**Summary:** By default, the first user created during Ubuntu installation is in the sudo group.

---

## Key Terms

|Term|Definition|
|---|---|
|**Built-in command**|A command implemented directly in the shell (e.g., `cd`).|
|**Executable**|A program stored on disk that can be run (e.g., `pwd`, `ls`).|
|**PATH**|An environment variable storing the default directories the shell searches for executables.|
