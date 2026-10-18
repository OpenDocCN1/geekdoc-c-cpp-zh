When the above code is compiled and executed, it produces the following result:

```
Here is the message: You wish!
```

# Parameterized Macros

One of the powerful functions of the CPP is the ability to simulate functions using parameterized macros. For example, we might have some code to square a number as follows:

```
```c
int square(int x) {

    return x * x;

}
```
```

We can rewrite the above code using a macro as follows:

```
```c
#define square(x) ((x) * (x))
```
```

Macros with arguments must be defined using the **#define** directive before they can be used. The argument list is enclosed in parentheses and must immediately follow the macro name. Spaces are not allowed between the macro name and open parenthesis. For example:

```
```c
#include <stdio.h>

#define MAX(x,y) ((x) > (y) ? (x) : (y))

int main(void)
{
    printf("Max between 20 and 10 is %d\n", MAX(10, 20));
    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
Max between 20 and 10 is 20
```