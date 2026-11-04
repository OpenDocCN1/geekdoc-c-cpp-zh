```
}

fputs(" \nTABLE OF SQUARES", fl);
fputs(" \n================\n", fl);

for(k = 1; k <= 5; k++)
{
    fprintf(fl, " %d\t%d\n", k, k*k);
}
fclose(fl);

return 0;
}
```

Figure 3.49 Program fsquares2.c

# Example 3.28

Write a program to read the contents of **squares.txt** created in the previous example and display it on the screen.

# Solution 3.28

Figure 3.50 shows the program listing (Program: **fdisp.c**). The program opens **squares.txt** in read mode. A **while** loop is used to read characters from the file using **getc** until the end-of-file (EOF) is reached. Function **putchar** displays the characters read from the file on the screen.

```
/*---------------------------------------------
        READING DATA FROM A FILE
        =========================

This program shows how data can be read from a file

Author: Dogan Ibrahim
File  : fdisp.c
Date  : December 2020
--------------------------------------------------*/

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int c;
    FILE *fl;
```