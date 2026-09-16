---
title: Multitasking & Context Switching
date: 2026-09-09
course: CS3620 Operating Systems
tags: [processes, multitasking]
related:
  - "[[Processes MOC]]"
  - "[[Process State & PCB]]"
  - "[[CPU Modes & Interrupts]]"
---

# Multitasking & Context Switching

## Implementation of Multitasking

> **Cues**
> - Implementation of multitasking
> - **Scheduler**
> - The three switching steps

- The part of the operating system that manages how CPU time is allocated to different processes is the **scheduler**.
	- The overhead of OS management should be as small as possible.

1. Save the state of the previous process.
2. Select a new process.
3. Load or initialize the state of the new process.

**Summary:** Switching runs in three steps — save the state of the previous process, select a new process, then load or initialize the state of the new process.

## How a Process Switch Actually Happens (Timer-Driven)

> Added from the Quiz 1 Study Guide — ties the three-step switch above to the hardware mechanism that triggers it (see [[CPU Modes & Interrupts]] for interrupts in general).

- A **hardware timer** triggers an interrupt every X ms.
- Inside the **timer interrupt handler**, the OS:
	1. Saves the state of the previous process
	2. Selects a new process
	3. Loads/initializes the new process's state

## Key Terms

- **Scheduler** — the part of the operating system that manages how CPU time is allocated to different processes.
