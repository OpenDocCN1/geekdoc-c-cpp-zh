Next, all open streams with unwritten buffered data are flushed, all open streams are closed, and all files created by the tmpfile are removed.

Finally, control is returned to the host environment. If the value of status is zero or EXIT_SUCCESS, an implementation-defined form of the status termination is returned. If the value of status is EXIT_FAILURE, an implementation-defined form of the status unsuccessful termination is returned. Otherwise the status is returned implementation-defined.

# Returns

The exit function cannot return to its caller.

# 7.22.4.5 The_Exit function

# Synopsis

```
#include <stdlib.h>
_Noreturn void _Exit(int status);
```

# Description

The _Exit function causes normal program termination to occur and control to be returned to the host environment. No functions registered by the atexit function, the at_quick_exit function, or signal handlers registered by the signal function are called. The status returned to the host environment is determined in the same way as for the exit function (7.22.4.4). Whether open streams with unwritten buffered data are flushed, open streams are closed, or temporary files are removed is implementation-defined.

# Returns

The _Exit function cannot return to its caller.

# 7.22.4.6 The getenv function

# Synopsis

```
#include <stdlib.h>
char *getenv(const char *name);
```

# Description

The getenv function searches an environment list, provided by the host environment, for a string that matches the string pointed to name. The set of environment names and the method for altering the environment list are implementation-defined. The getenv function need not avoid data races with other threads of execution that modify the environment list.