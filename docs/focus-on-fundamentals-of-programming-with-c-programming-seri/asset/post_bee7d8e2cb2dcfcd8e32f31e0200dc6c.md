
## The program below:

```c
// power3.c

#include <stdio.h>
#include <stdlib.h>

float power(float base, int expot);

int main(void) {
    float result = power(3.5, -6);
    printf("%f\n", result);
    return 0;
}

float power(float base, int expot) {
    int i;

    float num = 1.0;

    if (expot == 0) {
        return 1.0;
    }
    for (i = 0; i < abs(expot); ++i) {
        num *= base;
        if (expot >= 0) {
            return num;
        } else {
            return 1/num;
        }
    }
}
```

## produces the following output:

```
0.000544
```

Note the use of the abs() function that returns the absolute value of exponent is used in the for loop. The abs() function is a built-in C math function and its use requires the inclusion of the appropriate header file:

```c
#include <stdlib.h>
```

## Function Prototypes Revisited

In general, C does not care in what order you put your functions in the program, so long as the function name is known to the compiler before it is called. This is ensured through the use of function prototypes. A function prototype declares the function name, its parameters, and its return type to the rest of the program prior to the function's actual declaration.

Function prototypes are placed at the beginning of a program before the first function declaration, which is usually main(), and consists of the function header with a semicolon after the closing brace. Here's an example:

```c
// prototype.c

#include <stdio.h>

int main(void);
int add(int a, int b);
int mult(int a, int b);

int main(void) {
    int num1, num2;

    printf("Enter two integers: ");
    scanf_s("%d%d", &num1, &num2);
    printf("The sum of the two numbers is %d\n", add(num1, num2));
    printf("The product of the two numbers is %d\n", mult(num1, num2));
    return 0;
}

int add(int a, int b) {
    return a + b;
}

int mult(int a, int b) {
    return a * b;
}
```

## Here's the output of the program:

```
Enter two integers: 4 5
The sum of the two numbers is 9
The product of the two numbers is 20
```

Note that we even provide a function prototype for main().

Did you notice the & in front of num1 and num2 in the scanf_s() function?
When reading in an int, char, or float with scanf_s(), we must provide to scanf_s() not the variable name but the address of the variable in memory. & is referred to as the address of operator in C, and when placed in front of a variable, returns the address in memory of the variable.

## A Note on the Placement of main() and Function Prototypes...

Technically main() can be placed anywhere in a program. However, it is typically placed as the first function in a program. As you'll see, we generally do not place much detailed code in main(). When used correctly, it provides an abstraction to the rest of the program and its visibility as the first function in the program is useful.

But there's more to it than just style. Thinking that placing main() as the last function in a program will obviate the need for function prototypes is incorrect. Suppose your code was set up as follows:

```c
void foo1() {
...
}

void foo2() {
...
}

int main() {
...
}
```

If main() calls foo1() or foo2() there's no problem. If foo2() calls foo1() there's no problem. But what happens if foo1() calls foo2()? The compiler will complain because it has not yet seen the declaration for foo2(). What kind of a function is it? How many parameters does it have? What are the data types of the parameters? Are there any return values? How can the compiler do error checking on the function call to foo2() if it cannot answer all these questions?

The use of function prototypes allows the compiler to see the function declarations before any code is looked at so error checking can be performed properly.

Of course you might want to switch the order of foo1() and foo2() in your program and all would be well. However, in a large program with dozens of functions, it might not be so easy to order the functions properly. With the use of function prototypes, we never have to worry about the order of our functions.

One last reason for the use of function prototypes deals with the building of larger programs and linking source codes together. This will be a topic for discussion at a later time.

## Function Return Values

Note that even though a function returns a value, a program need not make use of it:

```c
// return1.c
while (...) {
    :
    getchar();    // get a character and do nothing with it
    c = getchar(); // get another character and assign to c
    :
}
```

## void Return Values and void Parameter List

If a function does not return any value, its return type should be specified as void. The void specifier informs the compiler that a function does not return a value. In a sense, the void data type is actually defining the absence of a data type and a function declared to be of type void has no return value and cannot be used in an expression as if it does.

```c
// return2.c
void printHeader(void) {
    printf("Program Number 1\n");
    printf("by Richard Stegman\n");
    printf("Version 5.0, released 10/12/18\n");
}
```

As you can see, this function returns no value. You can call it with the following statement:

```c
printHeader();
```

Note that you must include () in the call. If you do not, the function is not called, even though it will compile correctly on many systems.

If a function is not passed any parameters (i.e., there are no formal parameters declared), void should be specified in the parameter list within the parentheses after the function name. Here is a function that accepts no values and generates a random number between 0 and 255:

```c
// parameter1.c
int getRandomNumber(void) {
    return (rand() % 255);
}
```

The function header:

`int getRandomNumber(void)`

declares the function:

`getRandomNumber()`

to the rest of the program and specifies that the function will accept no parameters and will return an int result.

## Function Parameters

The value that is being passed to a function is called an argument or an actual parameter. The argument that appears in the function header is referred to as the formal parameter. We say that the actual parameter is passed to the formal parameter.

Function arguments are always passed by value in C. Each argument is evaluated and its value is used locally in place of the formal parameter in the function header. Therefore if an argument is passed to a function, the stored value of that argument will not be changed in the calling environment. For example:

```c
// parameter2.c

#include <stdio.h>

int main(void);
void foo(int num);

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

produces the following output:

```
5
5
6
5
```

If we want to pass an argument by *reference* (i.e., change the value of the argument in the function and have that new value be reflected back in the calling function), we must pass the *address* of the argument to the function, rather than the argument itself. Once the function has access to the memory location that is used to store the actual parameter, it can modify its contents, and thus modify the actual parameter.

For example:

```c
// parameter3.c

#include <stdio.h>

int main(void);
void foo(int *num);

int main(void) {
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

In order to pass by reference, we must first pass the address of the actual parameter to the function. This is accomplished by using the *address of operator* (&). When & is placed in front of a variable, it returns the address of that variable.
