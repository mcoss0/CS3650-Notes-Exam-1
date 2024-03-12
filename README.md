# CS3650-Notes-Exam-1
Notes for exam 1 of CS3650

## What are System Calls?

System calls are essential interfaces between user space applications and the kernel of an operating system. They provide a way for programs to request specific services or operations that the operating system kernel provides, such as process management, file operations, communication, and device manipulation. Below, I'll elaborate on some of the key system calls mentioned in the homework assignments and their purposes:

### 1. `fork()`
- **Usage**: `pid_t fork(void);`
- **Purpose**: Creates a new process by duplicating the calling process. The new process, referred to as the child, is an exact copy of the parent process except for the returned value.
- **Example Application**: It's commonly used to create a new process that executes a different program. In a typical scenario, a process might call `fork()` to create a new process and then use `execvp()` in the child process to run a new program.

### 2. `execvp()`
- **Usage**: `int execvp(const char *file, char *const argv[]);`
- **Purpose**: Replaces the current process image with a new process image specified by the file. This system call is part of the `exec` family, which allows a process to run any program files, which include binary executables or scripts.
- **Example Application**: After a process has called `fork()`, the child process might use `execvp()` to replace its image with that of another program. For example, running a shell command from a C program.

### 3. `open()`
- **Usage**: `int open(const char *pathname, int flags, mode_t mode);`
- **Purpose**: Opens a file or device, returning a file descriptor that can be used for reading, writing, or both, depending on the flags specified.
- **Example Application**: Opening a file to write the output of a command, as seen in the implementation of the `record` command in Homework 2.

### 4. `read()`
- **Usage**: `ssize_t read(int fd, void *buf, size_t count);`
- **Purpose**: Reads data from a file descriptor into a buffer. The file descriptor could refer to a file, a pipe, or a device.
- **Example Application**: Reading input from a file or standard input (stdin) and processing the data in the context of a cache simulator or other applications.

### 5. `dup2()`
- **Usage**: `int dup2(int oldfd, int newfd);`
- **Purpose**: Duplicates a file descriptor, making `newfd` be the copy of `oldfd`, closing `newfd` first if necessary.
- **Example Application**: Redirecting standard output or standard input to a file or pipe. This can be used to capture the output of a command into a file, as demonstrated in the `record` command implementation.

### 6. `pipe()`
- **Usage**: `int pipe(int pipefd[2]);`
- **Purpose**: Creates a pair of file descriptors, pointing to a pipe inode, which can be used for inter-process communication. Data written to `pipefd[1]` can be read from `pipefd[0]`.
- **Example Application**: Setting up a pipeline between processes, where the output of one process (e.g., a filter) can be used as the input for another process.

System calls are a critical part of systems programming, providing the mechanism for user-space applications to interact with the operating system and hardware. Understanding how to use these system calls is crucial for tasks ranging from simple file operations to complex process management and inter-process communication scenarios.
