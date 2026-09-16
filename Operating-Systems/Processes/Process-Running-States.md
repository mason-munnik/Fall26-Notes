---
title: Process Running States
date: 2026-09-14
course: CS3620 Operating Systems
tags: [processes, process-state]
related:
  - "[[Processes MOC]]"
  - "[[Process State & PCB]]"
  - "[[CPU Modes & Interrupts]]"
---

# Process Running States

## Process Running State

> From Lecture Sept 14.

A process can be in one of three states:

1. **Running** — the CPU is executing the process code.
2. **Ready** — the process is ready to run, but not currently on the CPU.
3. **Blocked** — the process is waiting for some I/O operation. When a process initiates an I/O request (e.g., write to a disk), it becomes blocked, and some other process can use the CPU.

**Summary:** A process is Running, Ready, or Blocked; a process blocks when it initiates an I/O request, freeing the CPU for another process.

## Key Terms

|State|Meaning|
|---|---|
|**Running**|CPU is actively executing this process's code|
|**Ready**|Process is ready to run but not currently on the CPU|
|**Blocked**|Process is waiting on I/O (e.g., a disk write); another process can use the CPU meanwhile|
