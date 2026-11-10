+   13.9  Write a program containing the function `str_reverse(s1, s2)` that reverses the case of letters in the string s1 and saves the converted string in s2. The function must also return a pointer to s2.

+   13.10  Write a program that accepts a string from the user and inserts a : as the delimiter after every five characters before printing the delimited string.

+   13.11  Write a program containing the function `str_replace(s, s1, s2)` that replaces the first occurrence of substring s1 with s2 in the string s. The function must return a pointer to s if the replacement is successful, or NULL otherwise. (HINT: Use the `strstr` function.)

+   13.12  Write a program to determine the character that occurs most in a user-input string.

+   13.13  Write a program that uses the `str_insert(s, s1, s2)` function to locate a substring s1 in string s and insert a substring s2 before s1. The function must return a pointer to s if the insertion is successful, or NULL otherwise.

+   13.14  Correct the errors in the following program which is meant to concatenate a string stg with another one specified as a command-line argument:

```
```c
#include <stdio.h>
#include <strings.h>
int main(int argc, char argv[])
{
    char stg[] = "ABCDEFGH";
    printf("Concatenated string = %s\n", strcat(stg, argv[0]));
    printf("Length of stg = %d\n", strlen(stg));
    return 0;
}
```
```

+   13.15  Write a program that splits a string on any of the delimiters stored in the string " |;:" (includes a space), and saves the words in a 2D char array. The program must accept a line of text from keyboard input and print each word on a separate line.

+   13.16  Write a program that sorts a set of five single-word strings input from the keyboard using a 2D char array and the bubble sort algorithm.

+   13.17  Develop a function named `str_compare(s1, s2)` which returns a positive integer if any character of string s2 occurs in s1. The function must return -1 on failure.

+   13.18  Correct the errors in the following program which is meant to accept an unspecified number of strings as command-line arguments and print them as a single concatenated string:

```
```c
#include <stdio.h>
#include <strings.h>
int main(int argc, char argv[])
{
    int i;
    char stg[300];
    char *s = stg;
    for (i = 0; i < argc; i++)
        s = strcat(s, argv[i]);
    printf("Concatenated string = %s\n", s);
    return 0;
}
```
```