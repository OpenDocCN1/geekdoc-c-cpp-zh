# Comparing Strings

# LISTING 18.6 stringcompare.c: Using strcmp() to Compare Strings

```
1: // stringcompare.c--The strcmp() function.
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: int main(void )
7: {
8:     char str1[80], str2[80];
9:     int x;
10:    while (1)
11:    {
12:
13:        /* Input two strings. */
14:
15:        printf("\nInput the first string, a blank to exit: %s");
16:        gets(str1);
17:
18:
19:        if ( strlen(str1) == 0 )
20:            break;
21:
22:        printf("\nInput the second string: %s");
23:        gets(str2);
24:
25:        /* Compare them and display the result. */
26:
27:        x = strcmp(str1, str2);
28:
29:        printf("\nstrcmp(%s,%s) returns %d", str1, str2, x);
30:    }
31:    return(0);
32: }
```

# Output

Input the first string, a blank to exit: **First string**

Input the second string: **Second string**

strcmp(First string,Second string) returns -1

Input the first string, a blank to exit: **test string**

Input the second string: **test string**

strcmp(test string,test string) returns 0