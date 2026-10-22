
```c
while (ct < LIM && s_gets(input[ct], SIZE) != NULL &&
        strcmp(input[ct], STOP) != 0)
{
    ct++;
}
printf("%d strings entered\n", ct);

return 0;
}

char * s_gets(char * st, int n)
{
    char * ret_val;
    int i = 0;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else // must have st[i] == '\0'
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

This program quits reading input when it encounters an EOF character (s_gets() returns NULL in that case), when you enter the word quit, or when you reach the limit LIM.

Incidentally, sometimes it is more convenient to terminate input by entering an empty line—that is, by pressing the Enter key or Return key without entering anything else. To do so, you can modify the while loop control statement so that it looks like this:

```c
while (ct < LIM && s_gets(input[ct], SIZE) != NULL
    && input[ct][0] != '\0')
```

Here, input[ct] is the string just entered and input[ct][0] is the first character of that string. If the user enters an empty line, s_gets() places the null character in the first element, so the expression

```c
input[ct][0] != '\0'
```

tests for an empty input line.

## The strncmp() Variation

The strcmp() function compares strings until it finds corresponding characters that differ, which could take the search to the end of one of the strings. The strncmp() function compares the strings until they differ or until it has compared a number of characters specified by a third argument. For example, if you wanted to search for strings that begin with "astro", you could limit the search to the first five characters. Listing 11.24 shows how.

### Listing 11.24 The starsrch.c Program

```c
/* starsrch.c -- use strncmp() */
#include <stdio.h>
#include <string.h>
#define LISTSIZE 6
int main()
{
    const char * list[LISTSIZE] =
    {
        "astronomy", "astounding",
        "astrophysics", "ostracize",
        "asterism", "astrophobia"
    };
    int count = 0;
    int i;

    for (i = 0; i < LISTSIZE; i++)
        if (strncmp(list[i], "astro", 5) == 0)
        {
            printf("Found: %s\n", list[i]);
            count++;
        }
    printf("The list contained %d words beginning"
           " with astro.\n", count);

    return 0;
}
```

Here is the output:

```
Found: astronomy
Found: astrophysics
Found: astrophobia
The list contained 3 words beginning with astro.
```

## The strcpy() and strncpy() Functions

We've said that if pts1 and pts2 are both pointers to strings, the expression

```c
pts2 = pts1;
```

copies only the address of a string, not the string itself. Suppose, though, that you do want to copy a string. Then you can use the strcpy() function. Listing 11.25 asks the user to enter words beginning with q. The program copies the input into a temporary array, and if the first letter is a q, the program uses strcpy() to copy the string from the temporary array to a permanent destination. The strcpy() function is the string equivalent of the assignment operator.

### Listing 11.25 The copy1.c Program

```c
/* copy1.c -- strcpy() demo */
#include <stdio.h>
#include <string.h>  // declares strcpy()
#define SIZE 40
#define LIM 5
char * s_gets(char * st, int n);

int main(void)
{
    char qwords[LIM][SIZE];
    char temp[SIZE];
    int i = 0;

    printf("Enter %d words beginning with q:\n", LIM);
    while (i < LIM && s_gets(temp, SIZE))
    {
        if (temp[0] != 'q')
            printf("%s doesn't begin with q!\n", temp);
        else
        {
            strcpy(qwords[i], temp);
            i++;
        }
    }
    puts("Here are the words accepted:");
    for (i = 0; i < LIM; i++)
        puts(qwords[i]);

    return 0;
}

char * s_gets(char * st, int n)
{
    char * ret_val;
    int i = 0;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else // must have st[i] == '\0'
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

The second argument is called the source. You can remember the order of the arguments by noting that it is the same as the order in an assignment statement (the target string is on the left):

```c
char target[20];
int x;
x = 50;                /* assignment for numbers */
strcpy(target, "Hi ho!"); /* assignment for strings */
target = "So long";      /* syntax error */
```

It is your responsibility to make sure the destination array has enough room to copy the source. The following is asking for trouble:

```c
char * str;
strcpy(str, "The C of Tranquility"); // a problem
```

The function will copy the string "The C of Tranquility" to the address specified by str, but str is uninitialized, so the copy might wind up anywhere!

In short, strcpy() takes two string pointers as arguments. The second pointer, which points to the original string, can be a declared pointer, an array name, or a string constant. The first pointer, which points to the copy, should point to a data object, such as an array, roomy enough to hold the string. Remember, declaring an array allocates storage space for data; declaring a pointer only allocates storage space for one address.

## Further strcpy() Properties

The strcpy() function has two more properties that you might find useful. First, it is type `char *`. It returns the value of its first argument—the address of a character. Second, the first argument need not point to the beginning of an array; this lets you copy just part of an array. Listing 11.26 illustrates both these points.

### Listing 11.26 The copy2.c Program

```c
/* copy2.c -- strcpy() demo */
#include <stdio.h>
#include <string.h>   // declares strcpy()
#define WORDS  "beast"
#define SIZE 40

int main(void)
{
    const char * orig = WORDS;
    char copy[SIZE] = "Be the best that you can be.";
    char * ps;

    puts(orig);
    puts(copy);
    ps = strcpy(copy + 7, orig);
    puts(copy);
    puts(ps);

    return 0;
}
```

Here is the output:

```
beast
Be the best that you can be.
Be the beast
beast
```

Note that strcpy() copies the null character from the source string. In this example, the null character overwrites the first `t` in `that` in `copy` so that the new string ends with `beast` (see Figure 11.5). Also note that ps points to the eighth element (index of 7) of copy because the first argument is copy + 7. Therefore, puts(ps) prints the string starting at that point.

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_513_0.png)

Figure 11.5 The strcpy() function uses pointers.

## The Careful Choice: strncpy()

The strcpy() function shares a problem with strcat()—neither checks to see whether the source string actually fits in the target string. The safer way to copy strings is to use strncpy(). It takes a third argument, which is the maximum number of characters to copy. Listing 11.27 is a rewrite of Listing 11.25, using strncpy() instead of strcpy(). To illustrate what happens if the source string is too large, it uses a rather small size (seven elements, six characters) for the target strings.

### Listing 11.27 The copy3.c Program

```c
/* copy3.c -- strncpy() demo */
#include <stdio.h>
#include <string.h>  /* declares strncpy() */
#define SIZE 40
#define TARGSIZE 7
#define LIM 5
char * s_gets(char * st, int n);

int main(void)
{
    char qwords[LIM][TARGSIZE];
    char temp[SIZE];
    int i = 0;

    printf("Enter %d words beginning with q:\n", LIM);
    while (i < LIM && s_gets(temp, SIZE))
    {
        if (temp[0] != 'q')
            printf("%s doesn't begin with q!\n", temp);
        else
        {
            strncpy(qwords[i], temp, TARGSIZE - 1);
            qwords[i][TARGSIZE - 1] = '\0';
            i++;
        }
    }
    puts("Here are the words accepted:");
    for (i = 0; i < LIM; i++)
        puts(qwords[i]);

    return 0;
}

char * s_gets(char * st, int n)
{
    char * ret_val;
    int i = 0;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else // must have st[i] == '\0'
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

Here's a sample run:

```
Enter your first name:
Annie
Enter your last name:
von Wurstkasse
Enter your prize money:
25000
von Wurstkasse, Annie        : $25000.00
```

The sprintf() command took the input and formatted it into a standard form, which it then stored in the string `formal`.

## Other String Functions

The ANSI C library has more than 20 string-handling functions, and the following list summarizes some of the more commonly used ones:

- `char *strcpy(char * restrict s1, const char * restrict s2);`
  This function copies the string (including the null character) pointed to by s2 to the location pointed to by s1. The return value is s1.

- `char *strncpy(char * restrict s1, const char * restrict s2, size_t n);`
  This function copies to the location pointed to by s1 no more than n characters from the string pointed to by s2. No characters after a null character are copied and, if the source string is shorter than n characters, the target string is padded with null characters. If the source string has n or more characters, no null character is copied. The return value is s1.

- `char *strcat(char * restrict s1, const char * restrict s2);`
  The string pointed to by s2 is copied to the end of the string pointed to by s1. The first character of the s2 string is copied over the null character of the s1 string. The return value is s1.

- `char *strncat(char * restrict s1, const char * restrict s2, size_t n);`
  No more than the first n characters of the s2 string are appended to the s1 string, with the first character of the s2 string being copied over the null character of the s1 string. The null character and any characters following it in the s2 string are not copied, and a null character is appended to the result. The return value is s1.

- `int strcmp(const char * s1, const char * s2);`
  This function returns a positive value if the s1 string follows the s2 string in the machine collating sequence, the value 0 if the two strings are identical, and a negative value if the first string precedes the second string in the machine collating sequence.

- `int strncmp(const char * s1, const char * s2, size_t n);`
  This function works like strcmp(), except that the comparison stops after n characters or when the first null character is encountered, whichever comes first.
