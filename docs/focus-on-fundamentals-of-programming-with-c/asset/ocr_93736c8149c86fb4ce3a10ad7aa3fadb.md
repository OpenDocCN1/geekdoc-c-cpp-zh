used to store the actual parameter, it can modify its contents, and thus modify the actual parameter.

For example:

```
#include <stdio.h>

int main(void):
void foo(int *num);
int num = 5;

    printf("%d\n", num);
    foo(&num);
    printf("%d\n", num);

    return 0;
}

void foo(int *num) {
    printf("%d\n", *num);
    *num = *num + 1;
    printf("%d\n", *num);
}
```

produces the following output:

```
5
5
6
6
```

Note that the value of the actual parameter has been changed by the call to foo().

In order to pass by reference, we must first pass the address of the actual parameter to the function. This is accomplished by using the address of operator (&). When & is placed in front of a variable, it returns the address of that variable.

So in the call from main():

```
foo(&num);
```