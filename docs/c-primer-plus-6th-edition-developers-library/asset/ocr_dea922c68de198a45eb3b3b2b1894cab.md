```
string++;
if (*string == '\0')
    return NULL;    /* NULL is the null pointer     */
else
    return string;
}
```

Here is a second solution that prevents the function from modifying the string but that allows the return value to be used to change the string. The expression (char *) string is called “casting away const.”

```
#include <stdio.h>    /* for NULL definition          */
char * strblk(const char * string)
{
    while (*string != ' ' && *string != '\0')
        string++;    /* stops at first blank or null */
    if (*string == '\0')
        return NULL;    /* NULL is the null pointer     */
    else
        return (char *) string;
}
```

# 13. Here is one solution:

```
/* compare.c -- this will work */
#include <stdio.h>
#include <string.h>  // declares strcmp()
#include <ctype.h>
#define ANSWER "GRANT"
#define SIZE 40
char * s_gets(char * st, int n);
void ToUpper(char * str);

int main(void)
{
    char try[SIZE];

    puts("Who is buried in Grant's tomb?");
    s_gets(try, SIZE);
    ToUpper(try);
    while (strcmp(try,ANSWER) != 0)
    {
        puts("No, that's wrong. Try again.");
        s_gets(try, SIZE);
        ToUpper(try);
    }
    puts("That's right!");
```