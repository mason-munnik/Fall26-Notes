---
title: CPU Virtualization & Process Concept
date: 2026-09-09
course: CS3620 Operating Systems
tags: [processes, cpu-virtualization]
related:
  - "[[Processes-MOC]]"
  - "[[Process-State-&-PCB]]"
  - "[[Multitasking-&-Context-Switching]]"
---

# CPU Virtualization & Process Concept

## Dividing CPU Time

> **Cues**
> - Dividing CPU time
> - Time slice
> - **Process**

- Main idea:
	- Divide the CPU by time division.
	- CPU time is divided into small time slices.
	- The CPU runs one program for one time slice, then switches to another program.
	- A program's code runs in a "virtual" environment called a **process**.

**Summary:** A program's code runs in a "virtual" environment called a process.

## Key Terms

- **Process** — the "virtual" environment a program's code runs in.
