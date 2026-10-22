the null character is the very first character in the ASCII sequence, s comes after it, and the function returns a positive value.

The last comparison points out that strcmp() compares all characters, not just letters, so instead of saying the comparison is alphabetic, we should say that strcmp() goes by the machine collating sequence. That means characters are compared according to their numeric representation, typically the ASCII values. In ASCII, the codes for uppercase letters precede those for lowercase letters. Therefore, strcmp("Z", "a") is negative.

Most often, you won’t care about the exact value returned. You just want to know if it is zero or nonzero—that is, whether there is a match or not—or you might be trying to sort the strings alphabetically, in which case you want to know if the comparison is positive, negative, or zero.

# Note

The strcmp() function is for comparing strings, not characters. So you can use arguments such as "apples" and "A", but you cannot use character arguments, such as 'A'. However, recall that the char type is an integer type, so you can use the relational operators for character comparisons. Suppose word is a string stored in an array of char and that ch is a char variable. Then the following statements are valid:

```
if (strcmp(word, "quit") == 0)  // use strcmp() for strings
    puts("Bye!");
if (ch == 'q')                  // use == for chars
    puts("Bye!");
```

However, don’t use ch or 'q' as arguments for strcmp().

Listing 11.23 uses the strcmp() function for checking to see whether a program should stop reading input.

# Listing 11.23 The quit_chk.c Program

```
/* quit_chk.c -- beginning of some program */
#include <stdio.h>
#include <string.h>
#define SIZE 80
#define LIM 10
#define STOP "quit"
char * s_gets(char * st, int n);

int main(void)
{
    char input[LIM][SIZE];
    int ct = 0;

    printf("Enter up to %d lines (type quit to quit):\n", LIM);
    while (ct < LIM && s_gets(input[ct], SIZE) != NULL &&
```