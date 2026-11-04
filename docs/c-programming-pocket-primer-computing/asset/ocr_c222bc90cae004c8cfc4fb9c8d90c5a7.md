However, if `str` contains multiple occurrences of the given delimiter, we would need to replace the while loop with the following code block:

```
```c
// print token after delimiter
while (token != NULL)
{
    token = strtok(NULL, delim);
    first = token;
    if(++count == 1) break;
}
```
```

The `main()` function initializes the array `names` with four names that are in reverse order (e.g., “Smith/John”). The next portion of the `main()` function contains a loop that iterates through the elements of the `names` array and invokes the function `tokenizeString()`. The output is here:

```
```text
NAME: jane smith
NAME: john edwards
NAME: dave stone
NAME: kenneth anderson
```
```

# POINTERS, STRINGS, AND PALINDROMES

A string is a palindrome if the reversed string is the same as the initial string. Listing 6.3 displays the contents of `StringPalindrome.c` that illustrates how to determine whether or not a string is a palindrome.

# LISTING 6.3: StringPalindrome.c

```
```c
#include <stdio.h>
#include <string.h>

int scanString(char str[])
{
```
```