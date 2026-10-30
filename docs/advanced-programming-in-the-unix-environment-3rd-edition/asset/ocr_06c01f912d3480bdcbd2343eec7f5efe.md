These minimum values do not change from one system to another. They specify the most restrictive values for these features. A conforming POSIX.1 implementation must provide values that are at least this large. This is why they are called minimums, although their names all contain MAX. Also, to ensure portability, a strictly conforming application must not require a larger value. We describe what each of these constants refers to as we proceed through the text.

> A strictly conforming POSIX application is different from an application that is merely POSIX conforming. A POSIX-conforming application uses only interfaces defined in IEEE Standard 1003.1-2008. A strictly conforming POSIX application must meet further restrictions, such as not relying on any undefined behavior, not using any obsolescent interfaces, and not requiring values of constants larger than the minimums shown in Figure 2.8.

| Name | Description | Minimum acceptable value |
|---|---|---|
| `ARG_MAX` | maximum length of arguments to exec functions | `POSIX_ARG_MAX` |
| `ATEXIT_MAX` | maximum number of functions that can be registered with the atexit function | 32 |
| `CHILD_MAX` | maximum number of child processes per real user ID | `_POSIX_CHILD_MAX` |
| `DELAYTIMER_MAX` | maximum number of timer expiration overruns | `_POSIX_DELAYTIMER_MAX` |
| `HOST_NAME_MAX` | maximum length of a host name as returned by gethostname | `_POSIX_HOST_NAME_MAX` |
| `LOGIN_NAME_MAX` | maximum length of a login name | `_POSIX_LOGIN_NAME_MAX` |
| `OPEN_MAX` | one more than the maximum value assigned to a newly created file descriptor | `_POSIX_OPEN_MAX` |
| `PAGESIZE` | system memory page size, in bytes | 1 |
| `RTSIG_MAX` | maximum number of real-time signal queues reserved for application use | `_POSIX_RTSIG_MAX` |
| `SEM_NSEMS_MAX` | maximum number of semaphores a process can use | `_POSIX_SEM_NSEMS_MAX` |
| `SEM_VALUE_MAX` | maximum value of a semaphore | `_POSIX_SEM_VALUE_MAX` |
| `SIGQUEUE_MAX` | maximum number of signals that can be queued for a process | `_POSIX_SIGQUEUE_MAX` |
| `STREAM_MAX` | maximum number of standard I/O streams a process can have open at once | `_POSIX_STREAM_MAX` |
| `SYMLOOP_MAX` | number of symbolic links that can be traversed during pathname resolution | `_POSIX_SYMLOOP_MAX` |
| `TIMER_MAX` | maximum number of timers per process | `_POSIX_TIMER_MAX` |
| `TTY_NAME_MAX` | length of a terminal device name, including the terminating null | `_POSIX_TTY_NAME_MAX` |
| `TZNAME_MAX` | number of bytes for the name of a time zone | `_POSIX_TZNAME_MAX` |

*Figure 2.9* POSIX.1 runtime invariant values from `<limits.h>`

Unfortunately, some of these invariant minimum values are too small to be of practical use. For example, most UNIX systems today provide far more than 20 open files per process. Also, the minimum limit of 256 for `_POSIX_PATH_MAX` is too small. Pathnames can exceed this limit. This means that we can’t use the two constants `_POSIX_OPEN_MAX` and `_POSIX_PATH_MAX` as array sizes at compile time.