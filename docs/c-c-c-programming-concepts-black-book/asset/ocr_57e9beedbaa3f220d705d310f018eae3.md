str1 until the count characters have been copied. If the string pointed to by str2 is longer than the count characters, then str1 will not be null-terminated. Listing 3.8 shows the working of strncpy():

# Listing 3.8: Showing the Working of the strncpy() Function

```
```c
#include<stdio.h>
#include<string.h>

int main()
{
    char str1[20];
    char str2[20];

    printf("\n Enter String 1 -> ");
    gets(str1);
    fflush(stdin);
    printf("\n Enter String 2 -> ");
    gets(str2);

    strncpy(str1, str2 , 10);

    printf("\n The result of the operation is -> %s", str1);

    getch()
    return 0;
}
```
```

Output of the preceding program is as follows:

```
```
Enter String 1 -> MY NAME IS TANUMAN

Enter String 2 -> THIS IS TEST

The result of the operation is -> THIS IS TE TANUMAN
```
```

# strcat()

The signature of the strcat() function is as follows:

```
```c
char *strncat(char *str1, const char *str2, size_t count);
```
```

The strncat() function concatenates up to the count characters of the string pointed to by str2 to the string pointed to by str1. This function also terminates str1 with a NULL. The NULL terminator at the end of str1 is overwritten by the first character of str2. The str2 string is unchanged by this operation. If the str1 and str2 strings overlap, then the behavior is undefined. Listing 3.9 shows the working of strncat():

# Listing 3.9: Showing the Working of the strncat() Function

```
```c
#include<stdio.h>
#include<string.h>

int main()
{
    char str1[20];
    char str2[20];

    printf("\n Enter String 1 -> ");
    gets(str1);
    fflush(stdin);
    printf("\n Enter String 2 -> ");
    gets(str2);
    strncat(str1, str2 , 10);
```
```