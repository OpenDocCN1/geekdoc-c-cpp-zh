
Can you find the error in the following program?

```c
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

## String Functions Revisited Using Pointers

The following two string functions return the number of characters in a string:

```c
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

The following four string functions copy string t into string s. Can you follow the pointers?

```c
// strcpy3.c
void strcpy(char s[], char t[]) {
    int i;
    for (i = 0; t[i] != '\0'; i++) {
        s[i] = t[i];
    }
    s[i] = '\0';
}
```

```c
// strcpy4.c
void strcpy(char *s, char *t) {
    for (; *t != '\0'; s++, t++) {
        *s = *t;
    }
    *s = '\0';
}
```

```c
// strcpy5.c
void strcpy(char *s, char *t) {
    while (*t) {
        *s++ = *t++;
    }
    *s = '\0';
}
```

```c
// strcpy6.c
void strcpy(char *s, char *t) {
    while (*s++ = *t++)
    ;
}
```

The following function concatenates string t onto the end of string s and returns
a pointer to the concatenated string:

```c
// strcat4.c
char *strcat(char *s, char *t) {
    while(*s) {
        s++;
    }
    while(*s++ = *t++) {
        ;
    }
    return s;
}
```

Note that in our final implementation of strcat(), we can actually return the
concatenated string as the function return value.

Finally, the following function compares two strings:

```c
// strcmp2.c
int strcmp(char *s, char *t) {
    while(*s == *t && *s) {
        s++;
        t++;
    }
    return *s - *t;
}
```

See if you can figure out the output to the following program:

```c
// doublep.c
#include <stdio.h>
void foo1(char *p);
void foo2(char **q);
int main(void) {
    char *p = "Hello";
    char *q = "Bye";
    printf("Function: main() ---> p = %s\n", p);
    foo1(p);
    printf("Function: main() ---> p = %s\n", p);
    printf("Function: main() ---> q = %s\n", q);
    foo2(&q);
    printf("Function: main() ---> q = %s\n", q);
    return 0;
}
void foo1(char *pp) {
    pp++;
    printf("Function: foo1() ---> pp = %s\n", pp);
}
void foo2(char **qq) {
    (*qq)++;
    printf("Function: foo2() ---> *qq = %s\n", *qq);
}
```

The output produced is as follows:

```
Function: main() ---> p = Hello
Function: foo1() ---> pp = ello
Function: main() ---> p = Hello
Function: main() ---> q = Bye
Function: foo2() ---> *qq = ye
Function: main() ---> q = ye
```

## Arrays of Character Strings

Consider the following array declaration:

```c
char name[5][10] = { "Haley", "Sammy", "Marc", "Lisa", "Zach" };
```

that sets up a rectangular two dimensional array of 5 rows each of length 10 columns. Note that it is necessary for us to declare a row's length large enough to at least hold the largest name:

![](img/0603fdf2eefeabaf26542250cc2fb439_352_0.png)

As you can see, this is a great waste of storage. Fortunately, C gives us the ability to declare an array with each row's length determined by the string it's initialized to:

```c
char *name[5] = { "Haley", "Sammy", "Marc", "Lisa", "Zach" };
```

Here, name is an array of 5 pointers to character strings. Each character string is an array of characters, so we have 5 pointers to arrays:

![](img/0603fdf2eefeabaf26542250cc2fb439_352_1.png)

The first pointer is name[0] and it points to the first string, the second pointer is name[1] and it points to the second string, etc. Note that each pointer points to the first character in each string:

```
*name[0] == 'H'
*name[1] == 'S'
*name[2] == 'M'
*name[3] == 'L'
*name[4] == 'Z'
```

This array of pointers is sometimes known as a ragged array, because each row may be of a different size. The ragged array, therefore, doesn't waste any storage space!

Consider the following example that declares a ragged array which stores various error messages which might be needed by a program:

```c
// arrayString.c

char *errorMsg[5] = { "Memory allocation error",
 "Stack overflow.",
 "Cannot read sector,",
 "File not found,",
 "Division by zero."
 };
```

To output an appropriate error message, it's simply a matter of accessing the appropriate array element:

```
puts(errorMsg[3]);
```

If we wanted to output all error messages contained within the ragged array, it would simply be a matter of iterating through the array:

```
for (i = 0; i < 5; i++) {
 puts(errorMsg[i]);
 }
```

## Command-Line Arguments

When a compiled program is executed, it's useful to supply initial values for some variables at runtime. These values are called command-line arguments. We have previously defined the main() function as:

```
int main(void);
```

but it is more generally defined as:

```
int main(int argc, char *argv[]);
```

The first argument, argc, stores the number of command-line arguments the program was invoked with (including the name of the program). The second argument, argv, is a pointer to ragged array of strings that stores the actual argument values passed to the program.

The declaration of argv:

```
char *argv[]
```

indicates that the pointer is to the initial element of the array and can also be written as:

```
char **argv
```

That is, argv is a pointer to a pointer to a char. If we look at the storage pointed to by argv, we will find an array of character pointers, each one pointing to a null-terminated string:

![](img/0603fdf2eefeabaf26542250cc2fb439_355_0.png)

### By convention:

- argc is at least one
- argv[0] is the name of the command itself (the name by which the program was invoked
- argv[1] points to the first argument string
- argv[2] points to the second argument string, etc
- argv[argc] is always the last element of the array and always contains a null pointer

For example, if we were to execute a program, foo, with two arguments:

```
foo arg1 arg2
```

the program will receive a value for argc equal to 3 and argv will look like:

![](img/0603fdf2eefeabaf26542250cc2fb439_355_1.png)

Within main(), the values on the original command-line can now be accessed and used like any other variable. We'll see shortly that we can also pass file names to main() from the command-line and open and access the contents of the files. The program below simply echoes its command-line arguments to the terminal window:

```c
// echo1.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    int i;

    for(i = 1; i < argc; i++) {
        printf("%s ", argv[i]);
    }
    printf("\n");

    return 0;
}
```

Since argv is a pointer to an array of pointers, we can rewrite the above program without using array indexing:

```c
// echo2.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    while(--argc > 0) {
        printf("%s ", *++argv);
    }
    printf("\n");
}
```

Since argv is a pointer to the beginning of the array of argument strings, incrementing it by 1, ++argv, makes it point at argv[1] instead of argv[0]. Each successive iteration moves it along to the next argument. *argv is then the pointer to that argument. When argc becomes 0, there are no arguments left.

The program below passes a file name on the command-line to main() and capitalizes and displays all letters in the file:

```c
// caps.c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

int main(int argc, char *argv[]) {
    int c;
    FILE *fp;

    if (!(fp = fopen(argv[1], "r"))) {
        puts("Could not open file.");
        exit(1);
    }

    while ((c = getc(fp)) != EOF) {
        if (islower(c)) {
            putchar(toupper(c));
        } else {
            putchar(c);
        }
    }

    return 0;
}
```

Our final example shows how flags can be used to modify commands. The flags are usually preceded by a hyphen and occur as the second argument on the command-line. The program below outputs its command-line arguments and if the flag -c is present, the arguments will be output in capital letters; otherwise the arguments will be output as they appear on the command-line. Note that the argument that contains the flag will not be output.

```c
// flag.c

#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
    int i = 1, flag = 0;

    if (!strcmp(argv[i], "-c")) {
        flag = 1;
        i = 2;
    }

    for ( ; i < argc; ++i) {
        if (flag) {
            strupr(argv[i]);
            printf("%s ", argv[i]);
        }
    }
    printf("\n");
    return 0;
}
```
