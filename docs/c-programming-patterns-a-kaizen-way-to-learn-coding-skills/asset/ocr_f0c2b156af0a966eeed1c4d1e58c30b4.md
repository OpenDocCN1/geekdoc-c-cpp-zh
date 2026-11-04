In a very loose term, the variable is basically made-up of three attributes. It has a name, data and memory address.

Let the `firstNum` and `secondNum` are the two variables declared in the `main()` method.

Let the variables `firstNum` and `secondNum` are having data values 9 and 10 respectively.

Let the memory address of variables `firstNum` and `secondNum` are 1000 and 1004 respectively.

# Call by Value

In this type of method call, the data value of a variable will be passed as an argument.

![](bbox=[0.1, 0.3, 0.9, 0.52])

Whenever there is a method call, every method will have it's own individual stack frame. Hence, when we execute the following program, each method `main()` and `swap()` will maintain a separate stack frame.

```
```c
#include <stdio.h>

void swap(int, int );// function prototype

int main() {

    // local variables: firstNum, secondNum

    int firstNum = 9, secondNum = 10;

    printf( "*** Before swap() method call ***\n");

    printf( "[firstNum = %d | secondNum = %d]\n", firstNum, secondNum );

    printf( "----------------------------------------------------\n");

    // actual arguments:firstNum, secondNum

    swap( firstNum, secondNum );

    printf( "----------------------------------------------------\n");

    printf( "*** After swap() method call ***\n");

    printf( "[firstNum = %d | secondNum = %d] ", firstNum, secondNum );

    return 0;

}
```
```