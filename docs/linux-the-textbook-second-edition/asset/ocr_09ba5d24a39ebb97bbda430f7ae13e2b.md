child process and the caller of fork() is known as the parent process. Both processes have their unique PIDs. Here is a brief description of the fork() system call.

```
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);

**Success:** 0 to the child process and the PID of child to the parent process
**Failure:** -1 and kernel variable errno set to indicate the type of error
```

As you can see, the fork() call returns a value of type pid_t. A combined reading of /usr/include/x86_64-linux-gnu/bits/types.h and /usr/include/x86_64-linux-gnu/bits/typesizes.h reveals that pid_t is a signed 32-bit integer. This means that you would use fork() in an assignment statement, as in

```
pid_t  pid;
...
pid = fork();
...
```

As soon as fork() has completed the creation of the child process and before it returns, the parent and child start running concurrently as independent processes. Both execute the statement following fork(), which is the assignment statement meant to save the return value of the fork() call. The fork() call returns 0 to the child process and the PID of the child process to the parent process. It is not easy to comprehend how a system call could return two values because a function may return only one value. Note that it is possible for fork() to return two values because as soon as the child process has been created, fork() has to complete its execution in both processes by returning a value in each of the two processes.

The child process inherits several attributes and characteristics of the parent process. Here is a partial list:

+   - A copy of the parent's PPFDT
+   - The current working directory
+   - The environment
+   - The root directory
+   - The set-UID (SUID) and set-group-ID (SGID) status
+   - The signal settings
+   - The time left before an alarm goes off
+   - The value of the file creation mask, umask

Although the child process is an exact copy of the memory image of the parent process, the two differ from each other in many ways:

+   - Both processes have their own PIDs.
+   - Both have different parent processes.
+   - Both have their own copies of the PPFDT.
+   - The resource utilization for the child process is set to 0.
+   - The child process has only one thread of execution, and if the parent process is multithreaded, the other threads do not release the resources held by them.

Since the parent and child processes have copies of the same PPFDT, both can do I/O with files that the parent process had opened before creating the child process, and this I/O is visible in both processes. In other words, the change is the position of the file pointer due to read(), write(), and lseek() calls by