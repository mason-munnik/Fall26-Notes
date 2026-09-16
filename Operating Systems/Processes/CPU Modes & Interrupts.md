---
title: CPU Modes & Interrupts
date: 2026-09-09
course: CS3620 Operating Systems
tags: [processes, interrupts]
related:
  - "[[Processes MOC]]"
  - "[[Multitasking & Context Switching]]"
  - "[[Process Running States]]"
---

# CPU Modes & Interrupts

## CPU Modes

> **Cues**
> - CPU modes
> - **User mode** vs **kernel mode**
> - Forbidden instructions
> - What triggers a mode change

- The CPU provides 2 different execution modes:
	- **User mode** (user programs)
	- **Kernel mode** (OS)
	- When the CPU is in user mode, some instructions are forbidden.
- The CPU is changed to kernel mode if an interrupt is triggered in the system.

**Summary:** The CPU is changed to kernel mode if an interrupt is triggered in the system.

## Interrupt

> **Cues**
> - **Interrupt**
> - What triggers an interrupt

- An **interrupt** is a mechanism for communication among the OS, user programs, and hardware.
- An interrupt is triggered if a forbidden or invalid instruction is executed in user mode:
	- e.g. access to some area of memory (e.g., `Load %addr, eax` is restricted to addresses in some memory range)
	- divide by zero

> [!warning] Verify
> The note treats a forbidden/invalid instruction, bad memory access, and divide-by-zero as *interrupts*. Standard x86 terminology calls these **exceptions** — synchronous events the CPU raises while executing an instruction — and reserves *interrupt* for asynchronous events from external devices ([Stanford i386 reference, §2.6](https://www.scs.stanford.edu/05au-cs240c/lab/i386/s02_06.htm)). Some texts do use "interrupt" as an umbrella term covering synchronous traps, so this may be the lecture's deliberate simplification. Confirm which convention the course uses before the exam.

- An interrupt can also be triggered by:
	- a system call, e.g. print
	- hardware, e.g. a keyboard (see the keyboard I/O walkthrough below)
- When an interrupt is triggered, the CPU:
	- switches to Kernel Mode
	- depending on the cause of the interrupt, jumps to a specific OS kernel location, according to the **Interrupt Table**

**Summary:** An interrupt can also be triggered by a system call, such as print, or by hardware, such as a keyboard.

### Interrupt Table

> Added from the Quiz 1 Study Guide.

`Interrupt Number → Address`, e.g.:

|Interrupt number|Cause|
|---|---|
|`0x1`|Invalid Memory Access|
|`0x2`|Division by Zero|
|`0x80`|System Call|
|`0x100`|Timer Interrupt|

A syscall like `int 0x80` causes the CPU to find entry `0x80` in the table and jump to that handler address.

### Hardware Input Example (Keyboard I/O Flow)

> From Lecture Sept 14.

- An interrupt can be triggered by hardware:
	- For instance: a peripheral communicates to the CPU when it finishes an operation.
	- When a disk finishes reading or writing data.
	- Every time you hit a key on the keyboard, an interrupt is triggered.

1. Trap to kernel mode.
2. Jump to interrupt handler.
3. Call device driver and read the character to kernel space.
4. Copy the character from kernel space to the user program.

## Key Terms

- **User mode** — the CPU execution mode for user programs, in which some instructions are forbidden.
- **Kernel mode** — the CPU execution mode for the OS.
- **Interrupt** — a mechanism for communication among the OS, user programs, and hardware.

## Corrections

Nothing was corrected — every checkable claim in this note verified as accurate.

**Flagged, not changed**

- "An interrupt is triggered if a forbidden/invalid instruction is executed in user mode … divide by zero" — standard x86 terminology classifies these as **exceptions** (synchronous, raised during instruction execution) rather than interrupts (asynchronous, from external devices), per the [Stanford i386 reference, §2.6](https://www.scs.stanford.edu/05au-cs240c/lab/i386/s02_06.htm). Left as written because "interrupt" is also used as an umbrella term for synchronous traps, and this may be the course's own framing. Confirm with the lecture slides.
