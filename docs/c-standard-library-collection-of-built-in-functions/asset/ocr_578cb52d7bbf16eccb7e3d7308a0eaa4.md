| S.N. | Macro & Description |
|------|---------------------|
| 1 | **SIGABRT**
Abnormal program termination. |
| 2 | **SIGFPE**
Floating-point error like division by zero. |
| 3 | **SIGILL**
Illegal operation. |
| 4 | **SIGINT**
Interrupt signal such as ctrl-C. |
| 5 | **SIGSEGV**
Invalid access to storage like segment violation. |
| 6 | **SIGTERM**
Termination request. |

# Library Functions

Following are the functions defined in the header signal.h:

| S.N. | Function & Description |
|------|------------------------|
| 1 | `void (*signal(int sig, void (*func)(int)))(int)`
This function sets a function to handle signal i.e. a signal handler. |
| 2 | `int raise(int sig)`
This function causes signal sig to be generated. The sig argument is compatible with the SIG macros. |

```
void (*signal(int sig, void (*func)(int)))(int)
```

# Description