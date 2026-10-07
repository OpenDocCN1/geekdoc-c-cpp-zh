The pointer ptr has been declared but not initialized. It points somewhere, but you don't know where. The gets() function doesn't know that ptr hasn't been initialized to point somewhere, so it simply goes ahead and stores the entered string at whatever address is contained in ptr. The string might overwrite something important, as program code or the operating system. Most compilers won't catch this type of mistake, so you, the programmer, must be vigilant.

# Syntax

# The gets() Function

```
#include <stdio.h>
char *gets(char *str);
```

The gets() function gets a string, str, from the standard input device, usually the keyboard. The string consists of any characters entered until a newline character is read. At that point, a null is appended to the end of the string.

Then the gets() returns a pointer to the string just read. If there is a problem getting the string, gets() returns null.

# Example

```
/* gets() example */
#include <stdio.h>
char line[256];int main( void )
{
    printf("Enter a string:\n");
    gets( line );
    printf("\nnYou entered the following string:\n\n" );
    printf("%s\n", line );
}
```

# Inputting Strings Using the scanf() Function

You saw in Lesson 7 that the scanf() library function accepts numeric data from the keyboard. This function can also input strings. Remember that scanf() uses a format string that tells how to read the information. To read a string, include the specifier %s in scanf()'s format string. Like gets(), scanf() is passed a pointer to the string's storage location.

How gets() decide where the string starts and ends? The end can be specified in the first nonwhitespace character encountered. If you use %s in the format string, the string runs up to (but not including) the next whitespace character (space, tab, or newline). If you use %ns (where n is an integer