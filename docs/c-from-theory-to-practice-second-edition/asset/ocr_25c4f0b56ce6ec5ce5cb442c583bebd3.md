The following program reads 50 names (less than 100 characters each) and stores them in different lines of a text file. Then, the program reads a character, reads the names from the file, and displays those that begin with the input character.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    FILE *fp;
    char ch, str[100];
    int i, times;

    fp = fopen("test.txt", "w+");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    for(i = 0; i < 50; i++)
    {
        printf("Enter name: ");
        read_text(str, sizeof(str), 1);
        fprintf(fp, "%s\n", str);
    }
    printf("Enter char: ");
    ch = getchar();

    fseek(fp, 0, SEEK_SET);
    times = 0;
    while(1)
    {
        if(fgets(str, sizeof(str), fp) == NULL)
            break;
        if(str[0] == ch)
        {
            printf("Name: %s\n", str);
            times++;
        }
    }
    printf("Total occurrences = %d\n", times);
    fclose(fp);
    return 0;
}
```
```