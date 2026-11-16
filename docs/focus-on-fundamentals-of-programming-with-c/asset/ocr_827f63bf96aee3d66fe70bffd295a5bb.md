# Example: Copy the contents of one file to another, line by line, and then output the new file.

```
#include <stdio.h>
#include <stdlib.h>

#define MAX 81

int main(void) {
    char line[MAX];
    FILE *fpin, *fpout;

    if (!((fpin = fopen("infile.txt", "r"))) {
        printf("File could not be opened for input.\n");
        exit(1);
    }
    if (!((fpOut = fopen("outfile.txt", "w"))) {
        printf("File could not be opened for output.\n");
        exit(1);
    }

    while (!feof(fpin)) {
        fgets(line, MAX, fpin);
        fputs(line, fpout);
    }
    fclose(fpin);
    fclose(fpOut);
    if (!((fpin = fopen("outfile.txt", "r"))) {
        printf("File could not be opened for input.\n");
        exit(1);
    }

    while (!feof(fpin)) {
        fgets(line, MAX, fpin);
        printf("%s", line);
    }

    return 0;
}
```