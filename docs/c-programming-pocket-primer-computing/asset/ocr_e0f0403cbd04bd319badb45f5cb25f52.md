The printf() function has the form printf(const char *format,...), and as you saw in [Chapter 1], this function writes output to the standard output stream according to the format that is specified in the specific invocation. For example, [Listing 2.16] displays the contents of PrintSamples.c that illustrates the use of the printf() function with various data types and formats.

# **LISTING 2.16: PrintSamples.c**

```
```c
#include <stdio.h>

int main()
{
    int x1 = 23;
    double x2 = 1234.56789;

    printf("Hello World\n");
    printf("%s\n", "Hello World");
    printf("%d\n", 17);
    printf("%s %d %5.2f\n", "Hello World", x1, x2);

    return 0;
}
```
```

[Listing 2.16] contains a main() function that initializes the variable x1 with 23 and the variable x2 with 1234.56789. The next section consists of four printf() statements that display various numbers and strings.

The format of the values that are displayed via the printf() function can be a simple constant string, but you can specify %s, %d, %c, %f, and so forth, in order to print or read strings, integer, character, or float respectively. There are many other formatting options available that you can use, based on your requirements. The output from [Listing 2.13] is here:

Hello World