# putchar()

putchar() outputs a single character to standard output (terminal window). The arguments to putchar() should be one individual character, either variable or constant:

```
putchar(c);
putchar('a');
putchar('\n');
```

If you just need to output a single character without format, use putchar() instead of printf(). Here's a program that copies its input to output:

```
// copy.c
#include <stdio.h>
int main(void) {
    int c;
    while ((c = getchar()) != EOF) {
        putchar(c);
    }
    return 0;
}
```

Note, if this program is applied to a file of 100 bytes, it will call getchar() 101 times. The first 100 calls will return a data byte. The 101st call will return the EOF value. Therefore the test is evaluated 101 times and the loop body is executed 100 times.

With this program we can write our own command line copy command using I/O redirection:

```
copy < inFile.txt > outFile.txt
```