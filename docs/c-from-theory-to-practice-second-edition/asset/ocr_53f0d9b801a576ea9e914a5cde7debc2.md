C.11.20 Write a function that takes as parameters two strings and uses them as pointers to copy the second one into the first one. Don't use strcpy(). Write a program that reads two strings of less than 100 characters and uses the function to swap them and display their content.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void copy(char s1[], char s2[]);
int read_text(char str[], int size, int flag);

int main(void)
{
    char str1[100], str2[100], tmp[100];

    printf("Enter first text: ");
    read_text(str1, sizeof(str1), 1);

    printf("Enter second text: ");
    read_text(str2, sizeof(str2), 1);

    copy(tmp, str1); /* Copy the first string into tmp. */
    copy(str1, str2); /* Copy the second string into str1. */
    copy(str2, tmp); /* Copy the first string into str2. */
    printf("\nFirst text: %s\n", str1);
    printf("Second text: %s\n", str2);
    return 0;
}

void copy(char s1[], char s2[])
{
    while(*s2 != '\0')
    {
        *s1 = *s2;
        s1++;
        s2++;
    }
    *s1 = '\0';
}
```
```

C.11.21 Write a function that takes as parameters two strings and returns 1 if the second string is contained at the end of the first one. Otherwise, it should return 0. Write a program that reads two strings of less than 100 characters and uses the function to check whether the second string is contained at the end of the first one or not.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int str_end(char str1[], char str2[]);
int read_text(char str[], int size, int flag);
```
```