value3: 1

As another example, consider the following code block that uses pointers in order to copy a string from the source (q) to the destination (p):

```
```c
void copy_string(char *p, char *q) {
    while (*p++ = *q++);
}
```
```

Although it’s possible to determine the purpose of the preceding code block, the following longer—yet equivalent—code is much easier to understand, maintain, and debug:

```
```c
void copy_string(char *dest, char *source)
{
    while (1) {
        *dest = *source;

        // Exit if we copied the end of string
        if (*dest == '\0') return;

        ++source;

        ++dest;
    }
}
```
```

Notice that the if statement and the return statement are on the same line. In this example, the code is so straightforward that there’s no possibility of confusion, which shows you that there can be exceptions to rules regarding code syntax.

# ERROR HANDLING IN C

Although C does not provide direct support for error handling, you can determine the results of program execution via return values. Recall that the main()