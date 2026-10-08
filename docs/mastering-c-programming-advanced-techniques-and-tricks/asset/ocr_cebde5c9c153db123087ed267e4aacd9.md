The following simple example demonstrates creating a new process using ‘fork()’ and identifying the parent and child processes based on the ‘fork()’ return value.

```
#include #include int main() { pid; = fork(); (pid == 0) // Child
process getpid()); else if (pid > 0) { // Parent process getpid(), pid); else {
Fork failed 1; 0; 
} }
```

Parent process: PID=4231, Child PID=4232
Child process: PID=4232

This example demonstrates how ‘fork()’ creates a child process and the differentiation between parent and child processes using ‘fork()’s return value.

# Example: Basic IPC using Pipes

Pipes are a fundamental IPC mechanism allowing unidirectional data flow between processes. The following example showcases a straightforward use of pipes to communicate between a parent and child process.

```
#include #include int main() { fd[2]; readbuffer[80];
(pipe(fd) = -1) { = fork(); (pid == 0) { Child process closes up input side
of pipe Send "Hello, parent!" through the output side of pipe 14); else {
Parent process closes up output side of pipe Read from the input
side of pipe readbuffer, sizeof(readbuffer)); readbuffer; 0; } }
```