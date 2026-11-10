```
int main(void)
{
    short i = 0, j;
    char stg[80];

    printf("Enter a string: ");
    scanf("%[^\n]", stg);          /* Only '\0' at end of stg, not '\n' */
    j = strlen(stg) - 1;             /* strlen is a library function */

    while (j) {
        if (stg[i++] != stg[j--]) {
            printf("%s is not a palindrome\n", stg);
            return 1;
        }
    }
    printf("%s is a palindrome\n", stg);

    return 0;
}
```

PROGRAM 13.5: **string_palindrome.c**

```
Enter a string: madam
madam is a palindrome

Enter a string: gentleman
gentleman is not a palindrome
```

PROGRAM OUTPUT: **string_palindrome.c**

# 13.7.2  count_words.c: Counting Number of Words in a String

Program 13.6 counts the number of words in a string, where a word is defined as a group of characters not containing whitespace (i.e., without spaces, tabs or newlines). The clever use of the variable flag ensures that multiple contiguous whitespace characters are treated as a single delimiter.

```
/* count_words.c: Counts number of words separated by any number
   of spaces, tabs and newlines. */
#include <stdio.h>
#define SIZE 80

int main(void)
{
    char stg[SIZE];
    short i = 0, flag = 1, count = 0;

    fputs("Enter a string: ", stdout);
    fgets(stg, SIZE, stdin);
```