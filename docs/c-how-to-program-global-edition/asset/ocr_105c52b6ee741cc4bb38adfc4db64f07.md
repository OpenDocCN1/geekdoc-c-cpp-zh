```
// Fig. 8.22: fig08_22.c
// Using function strpbrk
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char *string1 = "This is a test"; // initialize char pointer
    const char *string2 = "beware"; // initialize char pointer

    printf("%s\n%s\n%c%s\n%s\n",
           "Of the characters in ",
           string2,
           *strpbrk(string1, string2),
           " appears earliest in ", string1);
}
```

Of the characters in "beware"
'a' appears earliest in
"This is a test"

Fig. 8.22 | Using function strpbrk.

# 8.8.4 Function strrchr

Function strrchr searches for the last occurrence of the specified character in a string. If the character is found, strrchr returns a pointer to the character in the string; otherwise, strrchr returns NULL. Figure 8.23 shows a program that searches for the last occurrence of the character 'z' in the string "A zoo has many animals including zebras".

```
// Fig. 8.23: fig08_23.c
// Using function strrchr
#include <stdio.h>
#include <string.h>

int main(void)
{
    // initialize char pointer
    const char *string1 = "A zoo has many animals including zebras";

    int c = 'z'; // character to search for
    printf("%s\n%s%c%s\n",
           "The remainder of string1 beginning with the",
           "last occurrence of character ", c,
           " is: ", strrchr(string1, c));
}
```

The remainder of string1 beginning with the
last occurrence of character 'z' is: "zebras"

Fig. 8.23 | Using function strrchr.