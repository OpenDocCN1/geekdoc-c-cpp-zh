# Function Parameters

The value that is being passed to a function is called an *argument* or an *actual parameter*. The argument that appears in the function header is referred to as the *formal parameter*. We say that the actual parameter is passed to the formal parameter.

Function arguments are always passed *by value* in C. Each argument is evaluated and its value is used locally in place of the formal parameter in the function header. Therefore if an argument is passed to a function, the stored value of that argument will not be changed in the calling environment. For example:

```
```c
#include <stdio.h>

int main(void);
void Foo(int num);

int main(void) {
    int num = 5;
    printf("%d\n", num);
    foo(num);
    printf("%d\n", num);
    return 0;
}

int foo(int num) {
    printf("%d\n", num);
    num = num + 1;
    printf("%d\n", num);
}
```
```

produces the following output:

```
5
6
5
5
```

If we want to pass an argument *by reference* (i.e., change the value of the argument in the function and have that new value be reflected back in the calling function), we must pass the *address* of the argument to the function, rather than the argument itself. Once the function has access to the memory location that is