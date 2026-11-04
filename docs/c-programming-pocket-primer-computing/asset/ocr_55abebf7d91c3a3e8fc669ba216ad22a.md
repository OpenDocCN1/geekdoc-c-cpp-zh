# USING STRTOK() TO TOKENIZE A STRING

Consider the case of a string that has the form "Last/First", such as "Smith/John". The task is to split such a string into two separate strings: the string on the left side of the "/" symbol and the string on the right side of the "/" symbol. We can perform this task via the built-in C function strtok().

The strtok() function takes a pointer to a string (string_ptr) and a character to find (such as "/") as its arguments. Next, we employ a while loop that finds subsequent tokens in the remaining string.

Listing 6.2 displays the contents of Tokenize.c that illustrates how to split a string into tokens (i.e., individual words).

# LISTING 6.2: Tokenize.c

```
```c
#include <stdio.h>
#include <string.h>

char *delim = "/";

void tokenizeString(char *str)
{
    // first token = last name
    char *token = strtok(str, delim);
    char *second = token;
    char *first;
    int count = 0;

    // print token after delimiter
    while (token != NULL)
    {
        token = strtok(NULL, delim);
```
```