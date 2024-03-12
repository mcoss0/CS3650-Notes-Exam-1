
### Examples of System Calls Use Cases

#### 1. `fork()`
Creating a simple command-line shell where a new process is forked for each command entered by the user. The shell waits for the command to finish before accepting the next one.

```c
pid_t pid = fork();
if (pid == 0) {
    // Child process
    execvp(command, args); // Execute command
} else if (pid > 0) {
    // Parent process
    wait(NULL); // Wait for the child process to finish
}
```

#### 2. `execvp()`
Running a shell command from within a C program, replacing the current program's execution with the command's execution.

```c
char *args[] = {"ls", "-l", NULL};
execvp("ls", args); // This will run 'ls -l' in the current process
```

#### 3. `open()`
Opening a log file to write the output of a program.

```c
int fd = open("logfile.txt", O_WRONLY | O_CREAT | O_APPEND, 0644);
if (fd < 0) {
    perror("open");
    exit(EXIT_FAILURE);
}
```

#### 4. `read()`
Reading input from a file in a buffered manner, processing data in chunks.

```c
char buffer[1024];
int bytes_read;
int fd = open("input.txt", O_RDONLY);
if (fd < 0) {
    perror("open");
    exit(EXIT_FAILURE);
}

while ((bytes_read = read(fd, buffer, sizeof(buffer))) > 0) {
    // Process the data read into buffer
}
close(fd);
```

#### 5. `dup2()`
Redirecting the standard output of a program to a file, commonly used in implementing shell redirection.

```c
int fd = open("output.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
if (fd < 0) {
    perror("open");
    exit(EXIT_FAILURE);
}
dup2(fd, STDOUT_FILENO); // Redirect stdout to fd
close(fd); // No longer need the original fd
```

#### 6. `pipe()`
Setting up a pipeline where the output of one program feeds directly as input to another, similar to Unix pipes.

```c
int pipefd[2];
pipe(pipefd); // Create the pipe
pid_t pid = fork();

if (pid == 0) {
    // Child process
    close(pipefd[1]); // Close unused write end
    dup2(pipefd[0], STDIN_FILENO); // Replace stdin with read end of the pipe
    execvp("grep", grep_args); // Run grep as child
} else {
    // Parent process
    close(pipefd[0]); // Close unused read end
    write(pipefd[1], "data to search
", 15); // Send data through the write end of the pipe
    close(pipefd[1]); // Close write end, sending EOF to grep
    wait(NULL); // Wait for the child process to finish
}
```
