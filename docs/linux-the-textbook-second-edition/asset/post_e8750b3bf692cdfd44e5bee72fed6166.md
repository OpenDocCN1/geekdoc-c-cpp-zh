
## System Programming: Process Management and Signal Processing

```
/* Open file */
if (argc == 1) {
    printf("No file specified as command line argument.\n");
    exit(1);
}
if ((fd = open(argv[1], O_WRONLY|O_CREATE|O_TRUNC, S_IREAD|S_IWRITE)) == -1) {
    perror("File opening");
    exit(1);
}
/* Close standard output */
close(1);
/* Duplicate fd into file descriptor 1, i.e., stdout */
if (dup(fd) == -1) {
    perror("Duplicating file descriptor");
    exit(1);
}
/* Close fd in order to release the extra slot in the PPFD */
if (close(fd) == -1) {
    perror("File closing");
    exit(1);
}
/* Stdout redirected to the file passed as command line argument */
printf("Hello, world!\n");
    exit(0);
}
```

```
$ gcc -w dup.c -o dup
$ dup foo
$ cat foo
Hello, world!
```

In the following session, we show the use of dup2() in the dup2.c program to perform the same task as performed by the dup.c program—that is, redirect standard output to the file passed to the program as a command line argument.

```
#include <fcntl.h>
#include <sys/stat.h>

int main(int argc, char *argv[])
{
    int fd;
    /* Open file */
    if (argc == 1) {
        printf("No file specified as command line argument.\n");
        exit(1);
    }
    if ((fd = open(argv[1], O_WRONLY|O_CREATE|O_TRUNC, S_IREAD|S_IWRITE)) == -1) {
        perror("File opening");
        exit(1);
    }
    /* Duplicate fd into file descriptor 1, i.e., stdout */
    if (dup2(fd, 1) == -1) {
        perror("Duplicating file descriptor");
        exit(1);
    }
    /* Close fd in order to release the extra slot in the PPFD */
    if (close(fd) == -1) {
        perror("File closing");
        exit(1);
    }
}
```

```
/* Stdout redirected to the file passed as command line argument */
printf("Hello, world!\n");
exit(0);
}
```

```
$ gcc -w dup2.c -o dup2
$ dup2 foo
$ cat foo
Hello, world!
$
```

You can redirect standard input (or standard error) in the same manner as discussed. All three standard files may be redirected to one file or multiple files, one each for standard input, standard output, and standard error.

## Exercise 16.14

Replicate the preceding sessions on your system. Do the dup.c and dup2.c programs work as expected?

## 16.5 Getting the Attention of a Process: Linux Signals

Similar to how a peripheral device may use an interrupt to get the attention of the CPU and be served, you may use a signal to get the attention of a process. We discussed this topic in detail in Chapter 12 to explain signal/interrupt handling in shell scripts. Here, we discuss signal handling in a C program.

### 16.5.1 What Is a Signal?

As stated earlier, a signal in Linux vocabulary is an event that interrupts the execution of a process. We discussed the events that cause signals in Section 12.4 while discussing advanced Bourne shell programming. Some of the events that cause signals are listed in Table 12.1. We reproduce that table here as Table 16.8.

You can view the complete list of events that cause signals by viewing the man pages for the kill command or kill() system call. You can also use the kill -l command to display the list of signals.

## TABLE 16.8

Commonly Used Signals, Their Number, and Their Purpose

| Signal | Number | Purpose |
|---|---|---|
| SIGHUP (hang up) | 1 | Informs the process when the user who ran the process logs out and the process terminates |
| SIGINT (keyboard interrupt) | 2 | Informs the process when the user presses <Ctrl+C> and the process terminates |
| SIGQUIT (quit signal) | 3 | Informs the process when the user presses <Ctrl+|> or <Ctrl+\> and the process terminates |
| SIGKILL (sure kill) | 9 | Terminates the process with no further processing (e.g., exception handling) when the user sends this signal to it with the kill -9 command |
| SIGSEGV (segmentation violation) | 11 | Terminates the process upon memory fault when a process tries to access memory space that does not belong to it |
| SIGTERM (software termination) | 15 | Terminates the process when the kill command is used without any signal number |
| SIGTSTP (suspend/stop signal) | 18 | Suspends the process; usually <Ctrl+Z> |
| SIGCHLD (child finishes execution) | 20 | Informs the process of termination of one of its children |

## System Programming II: Process Management and Signal Processing

A similar list is also found in the /usr/include/x86_64-linux-gnu/asm/signal.h, /usr/include/asm-generic/signal.h, and /usr/src/linux-headers-4.4.0-21/include/uapi/asm-generic/signal.h files.

You can send a signal to a process by using the kill command or the kill() system call. Both take two arguments, a signal number and the PID of the process to receive the signal. For example, the kill -16 12345 command sends signal number 16 to the process with PID 12345.

### 16.5.2 Interception Signals

A process may use the sigaction() system call or the signal() library call to intercept a signal and take one of the following three possible actions:

- 1. Ignore the signal
- 2. Take the default action as defined by the kernel
- 3. Take the programmer-defined action

The default actions are listed in the /usr/src/linux-headers-4.4.0-21/include/linux/signal.h.

The interface for the sigaction() system call is rather complex. The library call signal() has a much simpler interface. For this reason, programmers normally use signal() for handling signals. Here is a brief description of this call:

```
#include <signal.h>
sig_t signal(int sig, sig_t func);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

The func argument is SIG_IGN for ignoring a signal and SIG_DFL for the default, kernel-defined action. A call to the signal() function may fail for two reasons, as shown in Table 16.9.

### 16.5.3 Setting Up an Alarm

The library call alarm() sends the SIGALRM signal to the calling process after the specified number of seconds. Thus, the call alarm(10) sends the SIGALRM signal to the caller process after 10 s. Here is a brief description of the call:

```
#include <unistd.h>
unsigned int alarm(unsigned int seconds);

Success: 0 if no alarm is currently set and the number of seconds left on the timer of the previous alarm()
Failure: -1 and kernel variable errno set to indicate the type of error
```

The maximum number of seconds allowed is 100,000,000. If an alarm has already been set but has not gone off (i.e., the signal has not been sent to the process), another call to alarm supersedes the previous call. The alarm(0) call cancels the current alarm and SIGALRM is never delivered to the calling process.

| Reason for Failure | Value of errno |
|--------------------|----------------|
| The signal specified in sig is not a valid signal number | EINVAL |
| The process tried to ignore or specify a handler for the SIGKILL or SIGSTOP signal | EINVAL |

```
[Output truncated]
16626 ?        00:00:00 sshd
16627 pts/0    00:00:00 bash
16647 pts/3    00:00:00 signals
16657 pts/0    00:00:00 ps
$ kill -1 16647
$ fg
signals
Waiting for alarm.
^CNice try! Sorry you cannot terminate me like this.
Waiting for alarm.
^Z
[1]+  Stopped                 signals
$ kill -9 16647
$ ps -U sarwar
PID TTY          TIME CMD
14466 ?        00:00:00 systemd
[Output truncated]
16626 ?        00:00:00 sshd
16627 pts/0    00:00:00 bash
16659 pts/3    00:00:00 ps
[1]+  Killed                 signals
$
```

On some Linux systems, the settings for intercepting signals using the signal() call is effective only once. When a signal has been intercepted and handled according to signal settings, the signal settings have to be reestablished in order for signal handling to work correctly. For this purpose, the relevant signal handlers include the code for resetting signals for future signal handling. For the signals.c program to work correctly on such systems, you need to modify the nicetry() function, the handler for SIGINT, as follows:

```
void nicetry(void)
{
    signal(SIGINT, nicetry);
    printf("Nice try! Sorry you cannot terminate me like this.\n");
}
```

## Exercise 16.15

Replicate the preceding sessions on your system. Does the signals.c program work as expected?

Several Internet services such as ftp are offered via server processes that provide services to client processes through multiple slave processes, one for each client. Slaves are precreated and/or created dynamically by the main server when needed. The main server is also known as the master server. Such servers are known as multiprocess servers or concurrent servers. A concurrent server runs in an infinite loop with the following code structure:

```
while (1) {
    wait for a client request
    create a slave process when a client request arrives
    slave handles the client request
}
```

Because concurrent servers keep creating slave processes as client requests arrive, it is important to terminate a slave process properly and remove it from the system after it has provided its service to a client process. This is done by using the exit() and wait() calls in tandem, in the slave and master processes, respectively. If the master server process does not remove the slave processes after they have provided
