```
long    sysconf(int name);
```

<unistd.h>
name: _SC_ARG_MAX, _SC_ASYNCHRONOUS_IO,
      _SC_ATEXIT_MAX, _SC_BARRIERS,
      _SC_CHILD_MAX, _SC_CLK_TCK,
      _SC_CLOCK_SELECTION, _SC_COLL_WEIGHTS_MAX,
      _SC_DELAYTIMER_MAX, _SC_HOST_NAME_MAX,
      _SC_IOV_MAX, _SC_JOB_CONTROL,
      _SC_LINE_MAX, _SC_LOGIN_NAME_MAX,
      _SC_MAPPED_FILES, _SC_MEMORY_PROTECTION,
      _SC_NGROUPS_MAX, _SC_OPEN_MAX,
      _SC_PAGESIZE, _SC_PAGE_SIZE,
      _SC_READER_WRITER_LOCKS,
      _SC_REALTIME_SIGNALS, _SC_RE_DUP_MAX,
      _SC_RTSIG_MAX, _SC_SAVED_IDS,
      _SC_SEMAPHORES, _SC_SEM_NSEMS_MAX,
      _SC_SEM_VALUE_MAX, _SC_SHELL,
      _SC_SIGQUEUE_MAX, _SC_SPIN_LOCKS,
      _SC_STREAM_MAX, _SC_SYMLOOP_MAX,
      _SC_THREAD_SAFE_FUNCTIONS,
      _SC_THREADS, _SC_TIMER_MAX,
      _SC_TIMERS, _SC_TTY_NAME_MAX,
      _SC_TZNAME_MAX, _SC_VERSION,
      _SC_XOPEN_CRYPT, _SC_XOPEN_REALTIME,
      _SC_XOPEN_REALTIME_THREADS, _SC_XOPEN_SHM,
      _SC_XOPEN_VERSION
Returns: corresponding value if OK, −1 on error

```
void    syslog(int priority, char *format, ...);
```

<syslog.h>

```
int     system(const char *cmdstring);
```

<stdlib.h>
Returns: termination status of shell

```
int     tcdrain(int fd);
```

<termios.h>
Returns: 0 if OK, −1 on error

```
int     tcflow(int fd, int action);
```

<termios.h>
action: TCOOFF, TCOON, TCOOFF, TCION
Returns: 0 if OK, −1 on error

```
int     tcflush(int fd, int queue);
```

<termios.h>
queue: TCIFLUSH, TCOFLUSH, TCIOFLUSH
Returns: 0 if OK, −1 on error