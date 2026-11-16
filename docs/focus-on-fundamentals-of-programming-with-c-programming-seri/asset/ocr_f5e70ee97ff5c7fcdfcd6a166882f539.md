Here's an example of the use of `scanf_s()`:

```
```c
// scanf_s.c

#include <stdio.h>

int main(void) {
    int i;
    double d;

    printf("Enter an integer and a double: ");
    scanf_s("%d %lf", &i, &d);
    return 0;
}
```
```

Input line:

```
250 123.45
```

The two input fields may be separated by as many blanks, tabs, and newlines (whitespace characters) as desired. `scanf_s()` skips any leading whitespace characters in the input (except when using the %c format specifier).

Any non-format characters specified in the format string of `scanf_s()` is to be expected on the input. For example, to enter the current time from terminal we can use:

```
scanf_s("%d:%d:%d", &hour, &min, &sec);
```

The : specifies that colons are expected as separators between the three integer values.

# Strings, characters, and scanf_s()

Microsoft has determined that any format string of the form "%s" is dangerous because it doesn't prevent buffer overflow (a security concern). This is why Microsoft uses the more secure `scanf_s()` function. In fact, if you are using Visual Studio and just use `scanf()`, the compiler will produce a warning message during the build phase.

So unlike `scanf()`, `scanf_s()` requires the buffer size to be specified for all input parameters of type c or s. The buffer size is passed as an additional