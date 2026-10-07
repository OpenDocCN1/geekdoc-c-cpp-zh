# Output ▼

source: The source string.
dest1: The source string.
dest2: The source string.

# Analysis ▼

This program demonstrates copying strings both to character arrays such as dest1 (declared on line 10) and to character pointers such as dest2 (declared along with dest3 on line 11). Line 13 prints the original source string. This string is then copied to dest1 with strcpy() on line 18. Line 24 copies source to dest2. Both dest1 and dest2 are printed to show that the function was successful. Notice that line 23 allocates the appropriate amount of space for dest2 with the malloc() function. If you copy a string to a character pointer that hasn’t been allocated memory, you get unpredictable results.

# The strcpy() Function

The strcpy function is similar to strcpy(), except that strcpy enables you to specify how many characters to copy. Its prototype is

char *strcpy(char *destination, const char *source, size_t n);

The arguments destination and source are pointers to the destination and source strings. The function copies, at the first n characters of source to destination. If source is shorter than n characters, null characters are added at the end of source to make a total of n characters copied to destination. If source is longer than n characters, terminating \0 is added to destination. The function’s return value is destination.

Listing 18.3 demonstrates the use of strcpy().

# Input ▼

LISTING 18.3 strcpy2.c: The strcpy() Function

```
/* strcpy2.c-Using the strcpy() function. */
2:
#include <stdio.h>
#include <string.h>
5:
char dest[] = "    ";
7:char source[] = "abcdefghijklmnopqrstuvwxyz";
9:
int main(void )
10:
```