# STRINGS

Syntax: strncpy(dest, source, number);

Where

destination
Pointer to the destination array where the content is to be copied.

source
C string to be copied.

number
Maximum number of characters to be copied from source.
Program 9.8 has used strncpy (), also see the null terminator is used.

```
# include <stdio.h>
# include <string.h>

int main () {
    char string1[13];
    char string2[13];
    strcpy(string1, "C PROGRAMMING");
    strncpy(string2, string1, 6);
    string2[7]=\0';
    printf("\n Source String %s \n",string1);
    printf("\n Destination String %s \n",string2);

    return 0;
}}
```

# Execution Result:

Source String C PROGRAMMING
Destination String C PROG

# Program 9.8 strncpy () utilization.

(d) strcat ()
This function helps the programmer with appending a copy of the source string to the destination string. The terminating null character in destination is overwritten by the first character of source string, and a new null-character is added at the end of the new string formed by the concatenation. Program 9.9 stands as a reference for strcat ().

```
# include <stdio.h>
# include <string.h>

int main () {
    char string1[20];
    strcpy(string1, "C PROGRAMMING");
    printf("\n Before strcpy %s",string1);
    strcat(string1, " IS EASY TO LEARN.");
    printf("\n After strcat %s",string1);
    getchar();
    return 0;
}
```

Execution Result:
Before strcat C PROGRAMMING
After strcat C PROGRAMMING IS EASY TO LEARN.

# Program 9.9 strcat () utilization.