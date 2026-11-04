We use fgets(), we'll see it later, to read a string and store it in str. Although it is allowed to call printf() in that way, printf() expects a pointer as its first argument, as shown in Appendix C, don't do that because if the character % is contained in the string, the compiler would interpret it as the beginning of a conversion specification and the behavior of the program would be unpredictable.

# Exercises

+   **C.10.2** Write a program that creates a string with all lowercase and uppercase letters of the English alphabet.

```
```c
#include <stdio.h>
int main(void)
{
    char str[53];
    int i;

    for(i = 0; i < 26; i++)
    {
        str[i] = 'a'+i;
        str[26+i] = 'A'+i;
    }
    str[52] = '\0'; /* At the end, we add the null character. */
    printf("%s\n", str);
    return 0;
}
```
```

**Comments:** In each iteration, the ASCII value of the respective character is stored in str. For example, in the first iteration (i=0), we have str[0] = 'a'+0 = 'a' = 97 and str[26] = 'A'+0 = 'A' = 65.

+   **C.10.3** What is the output of the following program?

```
```c
#include <stdio.h>
int main(void)
{
    char str[] = "Right\'0\'Wrong";

    printf("%s\n", str);
    return 0;
}
```
```