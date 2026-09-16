# System Calls
- A system call is a function provided by the OS that allows users to access system resources
- Linux process management is based on 3 system calls:
	- fork: create a new process
	- execve: load a program into a process
	- wait: wait for another process to finish

## Fork
- Fork creates a new process
	- Process A calls fork to create Process B
	- A is the parent process, B is the child process
- The new process is an exact copy of the old one
	- The only initial differences:
		- Process ID (pid)
		- The return value of fork
		- 