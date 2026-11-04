```
if(strcmp(str, max_str) > 0)
    strcpy(max_str, str);
}
printf("\nMax = %s Min = %s\n", max_str, min_str);
return 0;
}
```

# C.10.31 What is the output of the following program?

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str1[10], str2[] = "engine";
    printf("%c\n", ++str1[strcmp(strcpy(str1, "ine"), str2+3)+2]);
    return 0;
}
```

Answer: strcpy() copies the string "ine" into str1 and returns a pointer to str1. strcmp() compares the string pointed to by the return value of strcpy(), that is, str1. with the part of the string stored in the str2+3 position, that is, "ine". Since both strings are the same, strcmp() returns 0 and the program displays the value of ++str1[0+2]. Since str1[2] is 'e', the program outputs f.

# C.10.32

The data compression algorithm run length encoding (RLE) is based on the assumption that a symbol within the data stream may be repeated many times in a row. This repetitive sequence can be replaced by an integer that declares the number of repetitions and the symbol itself. Write a program that reads a string of less than 100 characters and uses the RLE algorithm to compress it. Don't compress digits and characters that appear once.

For example, the string: fffmmm1234jjjjjjjjjx should be compressed to 3f4m123410jx

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);
int main(void)
{
    char str[100];
    int i, len, cnt;
    printf("Original text: ");
    len = read_text(str, sizeof(str), 1);
    printf("Compressed text: ");
    i = 0;
    while(i < len)
    {
```