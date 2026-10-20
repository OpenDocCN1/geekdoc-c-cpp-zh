
## TABLE 16.2

Reasons for the fork() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The limit on the maximum number of processes that may run on the system simultaneously would be exceeded | EAGAIN |
| The limit on the maximum number of processes that may run under a user would be exceeded | EAGAIN |
| The resource limit set for the process has been reached | EAGAIN |
| Insufficient swap space for the new process | ENOMEM |

either process is visible in the other process. So, if either process reads N bytes from an already open file, the file pointer is incremented by N and the next read or write operation by parent or child is performed at the new position of the file pointer.

The fork() call may fail for the reasons listed in Table 16.2.

The vfork() system call is a lighter version of fork(). It creates a child process exactly like fork() but does not copy the address space of the parent; it copies the address space on demand—that is, when the child’s memory image is needed. The vfork() system call is used instead of fork(), particularly if the child process uses the execve() system call (or a variant) or the exec1() library call (or a variant) right after its creation to overwrite itself with another executable code. This is done in applications like a shell program that executes external commands by using and exec() call (exec1(), execve(), fexecve(), etc.) immediately after fork(). The exec() call is covered later in the chapter.

## Exercise 16.9

If you browse the man page for the fork() system call, you will see the names of the vfork() and rfork() calls. What is the purpose of each of these calls?

## 16.3.3 Reporting Status to the Parent Process

A Linux process reports its termination status to its parent via the _exit() system call or the exit() library call. Since most programmers use the exit() call to terminate a process, we will discuss it throughout the book. A process passes its termination status to its parent through the only parameter of the exit() call, usually, 0 or 1. The value 0 is used to indicate successful completion of the process and 1 means its unsuccessful termination.

The parent process accepts this status through the use of a system call in the wait() class (see Section 16.3.4). In reality, the status of the terminating process is saved in the proc structure of the process. All the data structures and resources allocated to the process are deallocated, except its proc structure. The proc structure is released back to the kernel after the parent has read the exit status of the child process. If a process does not use the exit() call to terminate itself, the kernel automatically sends the termination status of the process to its parent process.

Note that a child process and its parent rendezvous through the exit() and wait() system calls, with the parent receiving the exit status of the child and the reason for its termination through this meeting. This is the simplest form of interprocess communication available in Linux. By associating different connotations to the exit() parameter, the child can communicate meaningful messages to its parent. We discuss the issue of communication between Linux processes in detail in Chapter W20.

## 16.3.4 Collecting the Status of a Child Process

A process can use the wait() system call to wait for the termination of a child process and to know the reason of its termination. The process can use the waitpid() system call to wait for the termination of a particular child process. Here are brief descriptions of these system calls:

```
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *status);
pid_t waitpid(pid_t wpid, int *status, int options);

**Success:** PID of the child process
**Failure:** -1 and kernel variable errno set to indicate the type of error
```

The wait() call may fail for several reasons. Some of these reasons are listed in Table 16.3.

The programmer can decipher the termination status of a child process and additional information related to its termination, such as whether the process was terminated due to a signal, by examining the value of the status parameter. As shown in Figure 16.7, the exit status and the reason for the process to terminate are stored in status. The lower byte contains the reason for the process termination and the upper byte contains the exit status. If a process terminated on receiving a signal, the signal number is stored in the lower byte of the status variable. Thus, for example, if a process terminated due to <Ctrl+C> (keyboard interrupt), the lower byte contains SIGINT (i.e., value 2).

With the passage of time, Linux designers have added a number of variants of the wait() call. The wait() system call is the oldest, and waitpid() is the most restricted of these calls. The newest and broadest interface is the wait6() system call. Detailed discussions on wait3(), wait4(), and wait6() are beyond the scope of this book. Here are brief descriptions of the wait3() and wait4() calls:

```
#include <sys/types.h>
#include <sys/wait.h>
#include <sys/time.h>
#include <sys/resource.h>
pid_t wait3(int *status, int options, struct rusage *rusage);
pid_t wait4(pid_t wpid, int *status, int options, struct rusage *rusage);

**Success:** PID of the child process
**Failure:** -1 and kernel variable errno set to indicate the type of error
```

The wait4() system call instructs the process to wait for specific children processes and to retrieve the statistics about their resource usage. As shown in Table 16.4, the wpid parameter in the wait4() and waitpid() calls determines what child (or children) the parent process waits for.

The options argument in wait3() and wait4() contains a bitwise OR of any of the half a dozen options. You can see these options and their meaning by viewing the man pages for these calls and by browsing through the header file /usr/include/linux/wait.h or /usr/src/linux-headers-4.4.0-21/include/uapi/linux/wait.h. The man pages also describe several macros that you may use to determine the status of a terminated child process. For example, you can find out if a child process terminated due to the arrival of a signal and, if so, the number of the signal that caused the process to terminate. These macros are defined in the files /usr/include/x86_64-linux-gnu/sys/wait.h and /usr/include/x86_64-linux-gnu/bits/waitstatus.h.

When the WNOHANG option is specified and no processes are there to report the status, wait4() and wait3() do not block, and return 0 as the PID. Table 16.5 shows a few equivalences of the wait4() call and other calls in the wait() class.

## TABLE 16.3

Some of the Reasons for the wait() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The caller process has no children to wait for | ECHILD |
| The statuses from the terminated children are not available because the caller process is ignoring SIGCHLD and the system is discarding such statuses | ECHILD |
| The call was interrupted by a signal | EINTR |
| An invalid option was specified in the system call | EINVAL |

| Low byte | High byte |
|---|---|
| System's understanding of the reason for child's termination: zero for normal and nonzero for abnormal | Argument of the exit() call |
| 0 7 | 8 15 |

FIGURE 16.7 The meaning of the values in the two bytes of the value in the status parameter.

## TABLE 16.4

Values of the wpid Parameter for the wait4() and waitpid() System Calls and Children Processes Waited for

| wpid | The Caller Waits for |
|------|----------------------|
| -1 | Any child process |
| 0 | Any child process in the process group of the caller |
| > 0 | The child with PID wpid |
| < -1 | Any child process whose process GID equals the absolute value of wpid |

The fork.c program in the following session uses the fork() system call to create a child process. The child process terminates after displaying its PID and its parent PID. The parent process waits for the child process and terminates after displaying its PID and the child's PID. Note that the PID displayed by the parent is, as expected, the same as the parent PID displayed by the child process.

```
$ cat fork.c
#include <unistd.h>

extern int errno;

int main(void)
{
    int pid, status;

    pid = fork();
    if (pid == -1) {
        perror("Fork failed.");
        exit(1);
    }
    /* Child process */
    if (pid == 0) {
        printf("\nCHILD: Child here with PID = %d.\n", getpid());
        printf("CHILD: My Mom has PID = %d.\n", getppid());
        exit(0);
    }
    /* Parent process */
    wait(&status);
    printf("\nPARENT: Mom here with PID = %d.\n", getpid());
    printf("PARENT: Well done, child!\n\n");
    exit(0);
}
$ gcc -w fork.c -o fork
```

## TABLE 16.5

The Equivalences of the wait4() System Calls

wait4(..., ..., ..., 0);    waitpid(..., ..., ...);
wait4(-1, ..., ..., ...);    wait3(..., ..., ...);
wait4(-1, ..., 0, 0);       wait(...);
