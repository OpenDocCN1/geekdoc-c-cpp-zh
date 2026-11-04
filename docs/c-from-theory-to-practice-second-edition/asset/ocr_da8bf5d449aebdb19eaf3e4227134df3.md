the programmer knows that each line of the test.txt file contains a string of less than 100 characters, an integer and a double number, in order to pass the right arguments in fscanf().

```
```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
    char str[100];
    int i;
    double d;

    fp = fopen("test.txt", "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    while(1)
    {
        if(fscanf(fp, "%s%d%lf", str, &i, &d) != 3)
            break;
        printf("%s %d %f\n", str, i, d);
    }
    fclose(fp);
    return 0;
}
```
```

Like scanf(), fscanf() uses the space character to distinguish the read values.

> As with scanf(), be careful when using %s in fscanf() to read strings. If the string contains many words, only the first will be read.

Since stdin is associated with the keyboard by default, if we replace the first argument of fscanf() with stdin, a call of fscanf() is equivalent to a call of scanf(). For example, the following program uses fscanf() and fprintf(), instead of scanf() and printf(), to read an integer and a double number and display them.

```
```c
#include <stdio.h>
int main(void)
{
    int i;
    double d;

    fprintf(stdout, "Enter an integer and a double: ");
    if(fscanf(stdin, "%d%lf", &i, &d) == 2)
        fprintf(stdout, "%d %f\n", i, d);
    return 0;
}
```
```