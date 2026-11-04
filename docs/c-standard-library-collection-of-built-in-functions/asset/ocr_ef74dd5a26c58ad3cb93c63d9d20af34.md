```
#include <string.h>
#include <stdio.h>

int main()
{
    const char str[80] = "This is - www.tutorialspoint.com - website";
    const char s[2] = "-";
    char *token;

    /* get the first token */
    token = strtok(str, s);

    /* walk through other tokens */
    while( token != NULL )
    {
        printf( " %s\n", token );

        token = strtok(NULL, s);
    }

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
This is
www.tutorialspoint.com
website
```

# size_t strxfrm(char *dest, const char *src, size_t n)

# Description

The C library function size_t strxfrm(char *dest, const char *src, size_t n) transforms the first n characters of the string src into current locale and place them in the string dest.

# Declaration

Following is the declaration for strxfrm() function.