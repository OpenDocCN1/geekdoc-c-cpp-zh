Can you find the error in the following program?

```
// error.c

#include <stdio.h>

int main(void) {
    char *name;

    printf("Please enter your name: ");
    gets(name);
    printf("Hello %s\n", name);
    return 0;
}
```

# String Functions Revisited Using Pointers

The following two string functions return the number of characters in a string:

```
// strlen2.c

int strlen(char *s) {
    int i = 0;

    while(*s++) {
        i++;
    }
    return i;
}

// strlen3.c

int strlen(char *s) {
    char *ptr = s;

    while(*ptr) {
        ptr++;
    }
    return(ptr - s);
}
```