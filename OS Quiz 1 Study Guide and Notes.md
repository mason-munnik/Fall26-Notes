# CS:3620 Operating Systems

Covers: Intro to OS, Linux Shell, Processes, C Programming

---

## 1. Introduction to Operating Systems

### Core definition

- **OS**: system software that manages computer hardware/software resources and provides common services to programs.
- The OS sits between **programs** (top) and **hardware** (bottom), and **virtualizes** (abstracts) the hardware.

### Layered structure (know this diagram)

- **User space**: interpreted programs (Java/Python/.NET runtimes), native programs, browsers, system libraries (e.g., `libc`) → talk to the kernel through **system calls (syscalls)**.
- **Kernel space**: Network Manager, File Manager, Process Manager, Memory Manager, kernel modules, device drivers.
- **Hardware / Firmware**: bottom layer.

### Virtualization — the big idea

The OS takes a **physical resource** and turns it into a **virtual** version of itself. Virtual = more general/powerful/easy-to-use, sometimes less efficient (compatibility vs. performance tradeoff).

|Resource|Physical reality|Virtualized as|
|---|---|---|
|CPU|Few physical cores|Ability to run many programs "simultaneously" (time-slicing)|
|Memory|e.g. 8GB physical RAM|Can allocate far more (e.g. 25GB) virtual memory|
|Disk|Local disk, flash drive, remote disk|All appear uniformly as "files"|

### OS examples by device (be ready for a matching question)

- Laptop → Windows, macOS, Chrome OS, Linux, *BSD
- Web server → Linux, Windows, FreeBSD
- Smartphone → Android, iOS
- Home router → Linux
- PlayStation 4 / Nintendo Switch → FreeBSD

---

## 2. Linux Shell

### Shell basics

- Linux has a **graphical interface** and a **textual interface** (CLI/terminal).
- The **shell** is the program that provides the CLI; it lets you control and automate the machine.
- Prompt format: `user_name@machine_name:current_path$`

### Paths

- **Absolute path**: starts with `/`
- **Relative path**: relative to current working directory (`current_location + relative_path = absolute path`)
- Shortcuts: `.` = current dir, `..` = parent dir, `~` = home dir (`/home/<user_name>`)

### Command cheat sheet (high-yield — expect direct recall questions)

|Command|Purpose|
|---|---|
|`cd`|change directory|
|`ls`|list directory contents|
|`pwd`|print working directory (absolute path)|
|`cp` (`-r` for dirs)|copy files/folders|
|`mv`|move/rename files/folders|
|`mkdir`|create a directory|
|`cat`|print a text file|
|`echo "text"`|print text|
|`touch`|create an empty file|
|`vim`/`emacs`/`nano`|text editors|
|`find [path] [options]`|search for files (`-name`, `-type f/d`, `-size`, `-mtime`, `-exec ... \;`, `-maxdepth`)|
|`grep <pattern> <file>`|search text; `-i` ignore case, `-E` regex, `-v` invert match, `-B`/`-A` num context lines, `-C` num context both sides|
|`xargs`|apply a command to a list of inputs, e.g. `-n1 -P1 -I{}`|
|`which`|shows where an executable lives|
|`chmod +x <file>`|make a file executable (`g+x` = group)|
|`sudo <command>`|run as root (must be in sudoer/`sudo` group; check with `groups`)|
|`env`|show environment variables|
|`export VAR="value"`|set an environment variable (shell-local; put in `~/.bashrc` to persist)|

### Two types of commands

1. **Built-ins** (e.g. `cd`) — part of the shell itself.
2. **Executable programs on disk** (e.g. `pwd`, `ls`) — found via `PATH`; `which` shows the location.

- Running a local executable requires `./<executable>` and executable permission (`ls -la` to check `rwx` bits: 3 bits each for owner/group/other).

### PATH & environment variables

- `PATH` stores the default directories the shell searches for executables.
- `export VAR="value"` sets a variable for the current shell session only.
- Persist variables across shell launches by adding to `~/.bashrc`.

### Standard streams

- **stdin** (fd 0) — keyboard input by default
- **stdout** (fd 1) — printed to terminal by default
- **stderr** (fd 2) — printed to terminal by default

### Redirection

- `>` overwrite, `>>` append
- `ls > /tmp/file1` → redirect stdout to a file
- `ls 2> /tmp/file2` → redirect stderr to a file
- `strace ls 2>&1` → redirect stderr into stdout (merge streams)

### Pipes

- `command1 | command2` connects **stdout of command1 → stdin of command2**.

### Exit codes

- Every command returns an exit code; **0 = success**, stored in `$?` (check with `echo $?`).

### Chaining commands

- `cmd1 ; cmd2` — run cmd1 then cmd2 regardless of result
- `cmd1 && cmd2` — run cmd2 only if cmd1 succeeded (exit code 0)

### Scripting

- Starts with shebang `#!/bin/bash`
- Must be executable: `chmod +x <script>`
- Arguments accessed via `$1`, `$2`, `$3`, ...
- Supports variables, `if`, `for`, functions, etc.
- Example pattern to know: a `while true` loop with `sleep` for polling/monitoring scripts (connectivity checker used in lecture).

---

## 3. Processes

### Learning objectives (from the slides — likely exam framing)

1. What is a process?
2. What is an interrupt, and what triggers one?
3. How does the OS use interrupts to switch between processes?
4. What are the three running states of a process?

### Virtualizing the CPU

- **Problem**: few physical CPUs, but many programs need to "run at once."
- **Solution — time slicing**: CPU time is divided into small slices; the OS runs one program per slice then switches. A program's code running in this virtual environment is called a **process**.

### Process state

When the OS switches processes, it must save the outgoing process's state. State includes:

- **Memory**: stack (locals), heap (`malloc`/`mmap`), loaded libraries (e.g. `libc`)
    
- **Registers**: Instruction Pointer (PC), Stack Pointer (RSP), general-purpose registers (RAX, RBX, ...)
    
- Open files, network connections
    
- **PID** (process ID), **Parent PID**
    
- Security info (owner, permissions)
    
- All process states are stored in a doubly linked list called the **process list**.
    
- In Linux, the structure holding a process's state is called `task_struct`.
    

### Multitasking implementation (the switch cycle)

1. Save state of the previous process
2. Select a new process (scheduler)
3. Load/initialize the state of the new process

- Goal: keep OS management **overhead** as small as possible.

### CPU modes

- **User Mode**: runs user programs; some instructions are forbidden.
- **Kernel Mode**: runs the OS; full privileges.
- CPU switches to kernel mode when an **interrupt** is triggered.

### Interrupts

- An **interrupt** = mechanism for communication among OS, user programs, and hardware.
- Triggers:
    - A forbidden/invalid instruction in user mode (e.g., accessing restricted memory, divide by zero)
    - A **system call** (e.g., `print`)
    - **Hardware** (e.g., keyboard, disk finishing an I/O op)
- When triggered, the CPU:
    1. Switches to **Kernel Mode**
    2. Looks up the cause in the **Interrupt Table** (interrupt number → handler address) and jumps to that handler

### Interrupt table concept (know the lookup flow)

`Interrupt Number → Address` e.g. Invalid Memory Access = `0x1`, Division by Zero = `0x2`, System Call = `0x80`, Timer Interrupt = `0x100`. A syscall like `int 0x80` causes the CPU to find entry `0x80` in the table and jump to that handler address.

### How a process switch actually happens (timer-driven)

- A **hardware timer** triggers an interrupt every X ms.
- Inside the **timer interrupt handler**, the OS: (1) saves the state of the previous process, (2) selects a new process, (3) loads/initializes the new process's state.

### Hardware interrupt example (keyboard I/O flow)

1. Trap to kernel mode
2. Jump to interrupt handler
3. Call the device driver and read the character into kernel space
4. Copy the character from kernel space to the user program

### Three process running states (very likely a direct exam question)

|State|Meaning|
|---|---|
|**Running**|CPU is actively executing this process's code|
|**Ready**|Process is ready to run but not currently on the CPU|
|**Blocked**|Process is waiting on I/O (e.g., a disk write); another process can use the CPU meanwhile|

---

## 4. C Programming

### Why C?

- Directly interfaces with the kernel (syscalls) and hardware; direct memory control → performance.
- Most OS kernels are written in C.
- Drawback: easy to make hard-to-find mistakes, especially **memory corruption**.

### C vs Java (comparison — good for a "compare/contrast" question)

- Similar syntax; both have functions/methods, but **C is not object-oriented**.
- C: manual memory management (no garbage collector), manual string handling, **no array bounds checking**, uses **pointers** instead of object references.
- C compiles to an OS-specific binary format.

### Hello World / Compilation

```c
#include <stdio.h>
int main (int argc, char* argv[]){
    printf( "Hello world!\n" );
    return 0;
}
```

- Compile: `gcc -o hello hello.c`
- Run: `./hello`
- Compile & run in one line: `gcc -o hello hello.c && ./hello`

### Types (Linux, 64-bit) — memorize these sizes

|Type|Size|
|---|---|
|`char`|1 byte|
|`short`|2 bytes|
|`int`|4 bytes|
|`long`|8 bytes|
|`float`|4 bytes|
|`double`|8 bytes|
|`size_t`|8 bytes|

- `sizeof(<type>)` returns size in bytes.
- `short`/`int`/`long`/`char` can be **signed** (default) or **unsigned**.
- `signed int` range: −2,147,483,648 to 2,147,483,647
- `unsigned int` range: 0 to 4,294,967,295

### Variables & scope

- Declared with type + name; can be declared at function or global scope.
- Global variables persist and are visible across functions (see `global_variable++` example).

### Arrays

- `int a[5];` fixed-size array declaration.
- `int numbers[] = {1, 2, 3};` size inferred from initializer.
- **Key gotcha**: there is no built-in way to know the size of an array once you only have a pointer to it — you must track the length separately.

### printf format specifiers (high-yield memorization)

|Specifier|Type|
|---|---|
|`%d`|int|
|`%lu`|unsigned long|
|`%c`|char|
|`%s`|string (`char*`/`char[]`)|
|`%lx`|unsigned long, hex|
|`%p`|pointer/memory address, hex|

### Structs and typedef

```c
struct point { int x; int y; };
typedef unsigned char byte;
typedef struct line { int x1,y1,x2,y2; } line_type;
```

- Access members with `.` (e.g. `p.x`), or `->` when you have a pointer to a struct (`point->x` is shorthand for `(*point).x`).

### Functions

- Function **prototypes** must be declared before use, specifying parameter types and return type (`void` = no return value).
- **Passing semantics** (important exam concept):
    - **Primitive types and structs** are passed **by copy** (by value).
    - **Arrays** are passed **by reference** (decay to pointer).
    - To pass any other variable by reference, use a **pointer**.
- Example gotcha: `swap_variables(int a, int b)` (pass by value) does **not** swap the caller's variables; `swap_variables(int* a, int* b)` (pass by pointer) does.

### Pointers

- A pointer is a variable holding a **memory address**.
- Declare: `int* pointer;`
- Get address of a variable: `pointer = &variable;` (`&` = "address of")
- Dereference (access pointed-to value): `*pointer = 11;` (`*` = "follow the pointer")
- Trace-through exercises in the slides showed a pointer being reassigned between `var1` and `var2` and used to modify values indirectly — expect a similar trace question on the exam (draw the table: variable / address / value).

### Pointer arithmetic & arrays

- `array == &(array[0])` — array name decays to a pointer to its first element.
- If `int* pointer = array;`, then:
    - `pointer + index == &(array[index])`
    - `*(pointer + index) == array[index]`

### malloc / free

- `int* integers = (int*) malloc(10 * sizeof(int));` — allocate heap memory for 10 ints.
- `malloc` returns `void*`, so cast it to the type you need.
- **No garbage collector** — you must call `free(integers);` manually or leak memory.

### Strings

- A C string = array of `char` terminated by the **NULL byte** `'\x00'`.
- String literals (`"string"`) automatically get the NULL terminator.
- If you `malloc` space for a string, **allocate `strlen + 1` bytes** to leave room for the terminator.
- Common functions: `strcat`, `strlen`, `strncpy`.

### Linked lists

- Built manually with pointers: a `list_type` holds a `head` pointer; each `list_node` holds a `value` and a `next` pointer (NULL terminates the list).

### File I/O

- Standard library: `fopen`, `fclose`, `fread`, etc.
- Lower-level OS syscalls also available: `open`, `read`, `write`.

### gdb (debugger)

- Compile with no optimization + debug symbols: `gcc -O0 -ggdb -o program program.c`
- Launch: `gdb ./program`
- Key commands: `r` (run), `b` (breakpoint), `c` (continue), `n` (next line), `print <var>`, `bt` (backtrace/call stack)

---

## Quick Self-Check Questions

1. What does it mean that the OS "virtualizes" a resource? Give the CPU, memory, and disk examples.
2. List the layers from a user program down to hardware, including where syscalls happen.
3. Write the shell command to find all files containing "log" in a directory tree.
4. What's the difference between `>` and `>>`? Between `2>` and `2>&1`?
5. Explain the three process states and what causes a transition between each.
6. Walk through what happens, step by step, when a timer interrupt fires and the OS switches processes.
7. Why does `int 0x80` cause a jump into kernel code — what table is consulted?
8. In C, is a struct passed by value or reference? What about an array? What about with `malloc`?
9. Write a function that swaps two integers using pointers, and explain why the non-pointer version fails.
10. Why must you allocate `strlen(s) + 1` bytes when copying a string with `malloc`?