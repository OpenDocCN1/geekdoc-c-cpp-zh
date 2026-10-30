mean that the race condition doesn’t exist; it simply means that we can’t see it on this particular system.) The following actual output shows how the results can vary:

```
$ ./a.out
ooutput from child
utput from parent
$ ./a.out
ooutput from child
utput from parent
$ ./a.out
output from child
output from parent
```

We need to change the program in Figure 8.12 to use the TELL and WAIT functions. The program in Figure 8.13 does this. The lines preceded by a plus sign are new lines.

```
#include "apue.h"
static void charatatime(char *);

int
main(void)
{
    pid_t  pid;

+   TELL_WAIT();
+
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {  /* parent goes first */
+       WAIT_PARENT();
        charatatime("output from child\n");
    } else {
        charatatime("output from parent\n");
+       TELL_CHILD(pid);
    }
    exit(0);
}

static void
charatatime(char *str)
{
    char  *ptr;
    int   c;
    setbuf(stdout, NULL);      /* set unbuffered */
    for (ptr = str; (c = *ptr++) != 0; )
        putc(c, stdout);
}
```

Figure 8.13 Modification of Figure 8.12 to avoid race condition

When we run this program, the output is as we expect; there is no intermixing of output from the two processes.