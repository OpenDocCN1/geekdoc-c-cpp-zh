# Storage at the time the program terminates is allocated as follows:

| | 4 |
| str | P | P | P | P | P | P | P | P | P | P | P | \0 | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| strptr | A | A | A | A | A | A | A | \0 |
| | B | B | B | B | B | B | B | B | B | B | \0 |
| | E | E | E | E | \0 |
| | P | P | P | P | P | P | P | P | P | P | P | P | P | \0 |

With a maximum string length of 80 characters it would take 320 bytes of memory to store these strings in a static array. Using dynamic arrays, 48 bytes are needed for the strings, 80 more for the buffer, and 16 for the pointer array for a total of 144 bytes.

# 10.5.2 Passing Strings to Functions as Dynamic Arrays

A character string stored in dynamic storage may be passed to a function using the dynamic pointer and the string may be printed in the function. The following code shows the output of such a string.

```
#include <stdio.h>
void funcoutput(char *);
int main() {
	char str[20] = "COMPUTATION";
	char *chrptr;
	chrptr = (char *) malloc(strlen(str) + 1);
	strcpy(chrptr, str);
	funcoutput(chrptr);
	return 0;
}
```