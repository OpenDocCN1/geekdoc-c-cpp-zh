# Example

The program in Figure 8.1 demonstrates the fork function, showing how changes to variables in a child process do not affect the value of the variables in the parent process.

```
```c
#include "apue.h"

int     globvar = 6;        /* external variable in initialized data */
char    buf[] = "a write to stdout\n";

int
main(void)
{
        int     var;        /* automatic variable on the stack */
        pid_t   pid;

        var = 88;
        if (write(STDOUT_FILENO, buf, sizeof(buf)-1) != sizeof(buf)-1)
                err_sys("write error");
        printf("before fork\n");  /* we don't flush stdout */

        if ((pid = fork()) < 0) {
                err_sys("fork error");
        } else if (pid == 0) {          /* child */
                globvar++;
                var++;
        } else {                        /* parent */
                sleep(2);
        }

        printf("pid = %ld, glob = %d, var = %d\n", (long)getpid(), globvar,
               var);
        exit(0);
}
```
```

![](bbox=[0.147, 0.178, 0.926, 0.604])

If we execute this program, we get

```
```text
$ ./a.out
a write to stdout
before fork
pid = 430, glob = 7, var = 89    child's variables were changed
pid = 429, glob = 6, var = 88    parent's copy was not changed
$ ./a.out > temp.out
$ cat temp.out
a write to stdout
before fork
pid = 432, glob = 7, var = 89
before fork
pid = 431, glob = 6, var = 88
```
```

In general, we never know whether the child starts executing before the parent, or vice versa. The order depends on the scheduling algorithm used by the kernel. If it’s required that the child and parent synchronize their actions, some form of interprocess