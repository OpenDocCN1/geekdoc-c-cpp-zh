# 7.3  Process Termination

There are eight ways for a process to terminate. Normal termination occurs in five ways:

+   1. Return from main
+   2. Calling exit
+   3. Calling _exit or _Exit
+   4. Return of the last thread from its start routine (Section 11.5)
+   5. Calling pthread_exit (Section 11.5) from the last thread

Abnormal termination occurs in three ways:

+   6. Calling abort (Section 10.17)
+   7. Receipt of a signal (Section 10.2)
+   8. Response of the last thread to a cancellation request (Sections 11.5 and 12.7)

> For now, we’ll ignore the three termination methods specific to threads until we discuss threads in Chapters 11 and 12.

The start-up routine that we mentioned in the previous section is also written so that if the main function returns, the exit function is called. If the start-up routine were coded in C (it is often coded in assembly language) the call to main would look like

```
exit(main(argc, argv));
```

# Exit Functions

Three functions terminate a program normally: _exit and _Exit, which return to the kernel immediately, and exit, which performs certain cleanup processing and then returns to the kernel.

```
#include <stdlib.h>

void exit(int status);

void _Exit(int status);

#include <unistd.h>

void _exit(int status);
```

We’ll discuss the effect of these three functions on other processes, such as the children and the parent of the terminating process, in Section 8.5.

> The reason for the different headers is that exit and _Exit are specified by ISO C, whereas _exit is specified by POSIX.1.