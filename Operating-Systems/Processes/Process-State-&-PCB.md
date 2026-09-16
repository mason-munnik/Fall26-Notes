---
title: Process State & PCB
date: 2026-09-09
course: CS3620 Operating Systems
tags: [processes, process-state]
related:
  - "[[Processes-MOC]]"
  - "[[CPU-Virtualization-&-Process-Concept]]"
  - "[[Multitasking-&-Context-Switching]]"
---

# Process State & PCB

## Process State

> **Cues**
> - Process state
> - What the saved state includes
> - **Process list**
> - **task_struct**

- To switch between processes, the OS saves the state of a process when it is scheduled out.
- The state includes:
	- Memory
		- Stack (local variables, ...), Heap (malloc, mmap, ...), Loaded Libraries (libc, ...)
	- Registers
		- Instruction pointer (PC), Stack pointer (RSP), General purpose registers (RAX, RBX, ...)
	- Open files, network connections
	- Process ID (PID), Parent Process ID
	- Security information (process owner, permissions)
- The OS stores the states of all processes in a doubly linked list, called the **process list**.
- The data structure that stores the state of a process is called a **`task_struct`** in Linux.

**Summary:** The data structure that stores the state of a process is called a `task_struct` in Linux.

## Key Terms

- **Process list** — the doubly linked list in which the OS stores the states of all processes.
- **`task_struct`** — the name in Linux for the data structure that stores the state of a process.
