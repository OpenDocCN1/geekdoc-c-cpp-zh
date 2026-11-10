> **Note:** Unlike `fputs`, the `puts` function appends a trailing newline to the output. `puts` is normally not used with `fgets` because it creates double-spaced lines and it works only with `stdout`.

# 15.6.1　`fgets_fputs2.c`: Using fgets and fputs with a Disk File

Program 15.5 uses `fgets` to fetch a few lines from keyboard input. `fputs` writes these lines to the file foo. After `rewind` resets the file position indicator for foo to the beginning, `fgets` reads this file. The `rewind` function, which often eliminates the need to close and reopen a file, is discussed in Section 15.14.2.

```
/* fgets_fputs2.c: Saves and reads back user input to and from a file. */
#include <stdio.h>
#include <stdlib.h>
#define BUFSIZE 80

int main(void)
{
    FILE *fp;
    char buf[BUFSIZE];

    if ((fp = fopen("foo", "w+")) == NULL) {    /* File will also be read */
        perror("");
        exit(2);
    }

    fputs("Enter a few records, [Ctrl-d] to exit\n", stderr);
    while (fgets(buf, BUFSIZE, stdin) != NULL)
        fputs(buf, fp);

    rewind(fp);                         /* Positions indicator at beginning */

    fputs("\nReading from foo...\n", stderr);
    while (fgets(buf, BUFSIZE, fp) != NULL)
        fputs(buf, stdout);

    exit(0);
}
```

```
PROGRAM 15.5: `fgets_fputs2.c`

Enter a few records, [Ctrl-d] to exit
**fgets must be used in place of gets.**
**fputs should be used as the matching counterpart of fgets.**

Reading from foo...
fgets must be used in place of gets.
fputs should be used as the matching counterpart of fgets.
```

PROGRAM OUTPUT: `fgets_fputs2.c`