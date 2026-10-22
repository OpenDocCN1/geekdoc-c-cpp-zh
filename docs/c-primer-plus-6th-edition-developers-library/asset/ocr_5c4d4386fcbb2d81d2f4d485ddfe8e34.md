Your string twice (puts(), then fputs()):
apple pie

apple pie
Enter another string, please.
strawberry shortcake
Your string twice (puts(), then fputs()):
strawberry sh
strawberry shDone.

The first input, apple pie, is short enough that fgets() reads the whole input line and stores apple pie\n\0 in the array. So when puts() displays the string and adds its own newline to the output, it produces a blank output line after apple pie. Because fputs() doesn’t add a newline, it doesn’t produce a blank line.

The second input line, strawberry shortcake, exceeds the size limit, so fgets() reads the first 13 characters and stores strawberry sh\0 in the array. Again, puts() adds a newline to the output and fputs() doesn’t.

The fgets() function returns a pointer to char. If all goes well, it just returns the same address that was passed to it as the first argument. If the function encounters end-of-file, however, it returns a special pointer called the null pointer. This is a pointer guaranteed not to point to valid data so it can be used to indicate a special case. In code it can be represented by the digit 0 or, more commonly in C, by the macro NULL. (The function also returns NULL if there is some sort of read error.) Listing 11.8 shows a simple loop that reads and echoes text until fgets() encounters end-of-file or until it reads a blank line, indicated by the first character being a newline character.

# Listing 11.8 The fgets2.c Program

```
/* fgets2.c -- using fgets() and fputs() */
#include <stdio.h>
#define STLEN 10
int main(void)
{
    char words[STLEN];

    puts("Enter strings (empty line to quit):");
    while ((fgets(words, STLEN, stdin) != NULL && words[0] != '\n')
        fputs(words, stdout);
    puts("Done.");

    return 0;
}
```