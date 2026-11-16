The program below passes a file name on the command-line to main() and capitalizes and displays all letters in the file:

```
// caps.c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

int main(int argc, char *argv[]) {
    int c;
    FILE *fp;

    if (!(fp = fopen(argv[1], "r"))) {
        puts("Could not open file.");
        exit(1);
    }

    while ((c = getc(fp)) != EOF) {
        if (islower(c)) {
            putchar(toupper(c));
        } else {
            putchar(c);
        }
    }

    return 0;
}
```