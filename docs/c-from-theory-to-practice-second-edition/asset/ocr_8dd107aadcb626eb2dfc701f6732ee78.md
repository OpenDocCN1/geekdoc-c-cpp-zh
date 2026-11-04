Answer: Since the name of an array can be used as a pointer to its first element—we do know that we've written it many times, we just want to be sure that you've got it—str+4 is a pointer to the fifth character of str, that is, the null character. Therefore, the first strlen() returns 0. Since the string literal can be used as a pointer, the second strlen() returns the number of the characters after the second one. As a result, the program outputs: 0 3.

# C.10.16

Write a program that reads a string of less than 100 characters and displays it after replacing all 'a' characters that may appear at the beginning and at the end of the string with the space character. For example, if the user enters "aabcdaa", the program should display "  bcd  ", while if the input string is "bcdaa", the program should display "bcd  ".

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    char str[100];
    int i, len;

    printf("Enter text: ");
    len = read_text(str, sizeof(str), 1);

    for(i = 0; i < len; i++)
    {
        if(str[i] == 'a')
            str[i] = ' ';
        else
            break;
    }
    for(i = len-1; i >= 0; i--)
    {
        if(str[i] == 'a')
            str[i] = ' ';
        else
            break;
    }
    printf("Text: %s\n", str);
    return 0;
}
```

Comments: The first loop compares the characters in the beginning of the string with 'a'. If it is an 'a', it is replaced with the space character; otherwise, the loop is terminated. Similarly, the second loop replaces all 'a' characters at the end of the string with the space character.

# C.10.17

Write a program that reads continuously strings (less than 100 characters each). The program should copy each input string in a second string variable after replacing each single '*' with a double '**', and the lowercase letters with uppercase letters and