func = pick;

Here is a concrete example:

```
//include <stdio.h>
#include <string.h>

// forward declaration for the check function
// the third parameter is a function pointer
void check(char *a, char *b, int (*cmp)(const char *, const char *));

int main(void)
{
    char s1[80] = "hello world"
    char s2[80] = "bye"

    // declare a function pointer p
    int (*p)(const char *, const char *);

    // assign the strcmp library function to p
    p = strcmp;
    check(s1, s2, p);
    return 0;
}

void check(char *a, char *b, int (*cmp)(const char *, const char *))
{
    printf("Testing for equality.\n");

    if (cmp(a, b)) printf("Equal");
    else printf("Not Equal");\}
```

implementation of the check function

The check() function is called, two character pointers and one function pointer are passed as arguments. Inside check(), the expression (*cmp)(a, b) calls strcmp(), which is pointed to by cmp, with the arguments a and b.