```
char *substr(char *s, short start, short length)
{
    static char stg[20];
    short i, j = 0;

    if (start + length > strlen(s))  /* If substring goes past array end */
        return NULL;
    else {
        for (i = start; i < start + length; i++)
            stg[j++] = s[i];
        stg[j] = '\0';
        return stg;
    }
}
```

# PROGRAM 13.9: **substr.c**

```
Enter index and length of substring: **0 6**
Substring is JanFeb
Enter index and length of substring: **33 3**
Substring is Dec
Enter index and length of substring: **33 4**
Illegal arguments
```

PROGRAM OUTPUT: **substr.c**

# 13.9  STANDARD STRING-HANDLING FUNCTIONS

Unlike C++ and Java, which have strong string-handling capabilities, C supports a limited number of string-handling functions. An enlarged list of functions supported by the standard library is available in Appendix A. Table 13.2 lists a subset of these functions which are discussed in the following sections. They are presented here with their prototypes and code snippets that highlight their usage. All of them need the **#include <string.h>** directive.

# 13.9.1  The strlen Function

Prototype:  `size_t strlen(const char *s);`

```
printf("Enter string: ");
scanf("%[\n]", stg1);
printf("Length: %hd\n", strlen(stg1));
```

> If input is Burundi ...
> ... printf displays 7

The **strlen** function returns the length of the string without the NUL character. The value returned is of type size_t, which is an unsigned type guaranteed to return at least 16 bits.

# 13.9.2  The strcpy Function

Prototype:  `char *strcpy(char *dest, const char *src);`

```
strcpy(stg2, stg1);
printf("Copied string: %s\n", stg2);
```

> Copies stg1 to stg2
> Also prints Burundi