where line is the line we're breaking into words, words is the array to be filled in with the (pointers to the) words, and nwords (the return value from getwords) is the number of words which the function finds. (As with getline, we tell the function the size of the array so that if the line should happen to contain more words than that, it won't overflow the array).

Here is the definition of the getwords function. It finds the beginning of each word, places a pointer to it in the array, finds the end of that word (which is signified by at least one whitespace character) and terminates the word by placing a '\0' character after it. (The '\0' character will overwrite the first whitespace character following the word.) Note that the original input string is therefore modified by getwords: if you were to try to print the input line after calling getwords, it would appear to contain only its first word (because of the first inserted '\0').

```
#include <stddef.h>
#include <ctype.h>
getwords(char *line, char *words[], int maxwords)
{
char *p = line;
int nwords = 0;

while(1)
{
while(isspace(*p)) p++;

if(*p == '\0')
return nwords;
words[nwords++] = p;
```