# Syntax

# The printf() Function

```
#include <stdio.h>
printf(format-string,arguments,...);
```

printf() is a function that accepts a series of arguments, each applying to a conversion specifier in the given format string. printf() prints the formatted information to the standard output device, usually the display screen. When using printf(), you need to include the standard input/output header file, stdio.h. The format-string is required; however, arguments are optional. For each argument, there must be a conversion specifier. Table 7.2 lists the most commonly used conversion specifiers.

The format-string can also contain escape sequences. Table 7.1 lists the most frequently used escape sequences.

The following are examples of calls to printf() and their output:

# Example 1 Input

```
#include <stdio.h>
int main( void )
{
printf("This is an example of something printed!");
    return 0;
}
```

# Example 1 Output

This is an example of something printed!

# Example 2 Input

printf("this prints a character, %c\n number, %d\n floating \npoint, %%f", 'z', 123, 456.789);

# Example 2 Output

This prints a character, z
a number, 123
a floating point, 456.789

> You may notice in the second example, the printf() function uses a string that wraps to a second line. At the end of the first line, a forward slash (\) indicates the string continues to the next line. The compiler treats the two lines as one.