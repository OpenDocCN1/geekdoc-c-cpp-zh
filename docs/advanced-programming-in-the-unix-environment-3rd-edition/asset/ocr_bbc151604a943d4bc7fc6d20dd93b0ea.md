Figure B.2 summarizes the differences between the various error functions.

| Function | Adds string from strerror? | Parameter to strerror | Terminate? |
|---|---|---|---|
| `err_dump` | yes | errno | abort(); |
| `err_exit` | yes | explicit parameter | exit(1); |
| `err_msg` | no |  | return; |
| `err_quit` | no |  | exit(1); |
| `err_ret` | yes | errno | return; |
| `err_sys` | yes | errno | exit(1); |
| `err_cont` | yes | explicit parameter | return; |
| `log_msg` | no |  | return; |
| `log_quit` | no |  | exit(2); |
| `log_ret` | yes | errno | return; |
| `log_sys` | yes | errno | exit(2); |
| `log_exit` | yes | explicit parameter | exit(2); |

Figure B.2  Our standard error functions

Figure B.3 shows the error functions that output to standard error.

```
```c
#include "apue.h"
#include <errno.h>       /* for definition of errno */
#include <stdarg.h>      /* ISO C variable arguments */

static void err_doit(int, int, const char *, va_list);

/*
 * Nonfatal error related to a system call.
 * Print a message and return.
 */
void
err_ret(const char *fmt, ...)
{
        va_list         ap;

        va_start(ap, fmt);
        err_doit(1, errno, fmt, ap);
        va_end(ap);
}

/*
 * Fatal error related to a system call.
 * Print a message and terminate.
 */
void
err_sys(const char *fmt, ...)
{
        va_list         ap;

        va_start(ap, fmt);
        err_doit(1, errno, fmt, ap);
        va_end(ap);
}
```
```