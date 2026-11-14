
![](img/679b8d2d47f1bf86e17aca48f596f5cc_364_0.png)

### Figure 7.19 Returning Data from a Function via the Stack

When the program is compiled, the body of the function will be stored in memory much as is seen in Figure 7.20. The key point here is that the code comprising the body of the function has an address and, in this example, that address is 0x6FAC. We will work more with such addresses shortly.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_364_1.png)

### Figure 7.20 The Function Body in Memory

Observe that only the implementation portion of the function is stored. The parameters passed in and, thus, the local variables are stored on the stack.

## 7.4.3 Pass By Value

*pass by value* In the program just described, we stressed that the variables passed into and returned from the function were copies of the original variables. The C language is called a pass by value language. This means that although the variables inside the body of the function have the same values as the originals, they are not the original variables. Consequently, any changes made to those values while in the function body are not reflected in the original variables; the original variables are in a different local scope.

The same is true for any variables declared within the function body; such variables cannot be accessed in the original calling function. Once again, the local scopes are different. If we return such a variable, we are only returning its value. Any variables declared within the function body are not valid as soon as the enclosing scope is exited.

The pass by value semantics of the C language is a very good source of programming bugs. The common lament is, “I made a change to the variable, I can see the change, but it still has the original values back here. ... I don’t understand this.” The code module in Figure 7.21 will illustrate the problem.

### EXAMPLE 7.14

```c
#include <stdio.h>
/*
Demonstrate pass and return by value in C
*/
int myFunction(int aValue);
void main(void)
{
    // declare and initialize some working variables
    int myValue = 5;
    int aReturnVal = 0;
    myFunction(myValue);
    // will show myValue as 5...no change
    printf("main(): myValue is: %d\n", myValue);
    // will show aReturnValue as 0...no change
    printf("main(): aReturnVal is: %d\n", aReturnVal);
    // by assigning to aReturnValue, we copy the returned value
    aReturnVal = myFunction(myValue);
    // will show aReturnValue as 9
    printf("main(): aReturnVal is: %d\n", aReturnVal);
    return;
}
int myFunction(int myValue)
{
    // declare and initialize a working variable
    int aReturnVal = 0;
    // change the value of the input parameter
    // this change will not appear in main
    myValue = myValue + 4;
    // will show myValue as 9
    printf("myFunction(): aValue is: %d\n", myValue);
    aReturnVal = myValue;
    return aReturnVal;
}
```

### Figure 7.21 Passing to a Function by Value

myFunction() As is evident, any changes made to the variables passed in to myFunction() are visible only while within the scope of that function, even if the same names are used as in the calling function.

## 7.4.4 Pass By Reference

Although C is a pass by value language by default, it is sometimes necessary to be able to pass the original variables into a function, operate on those variables, and have the results persist outside of the function. Under such circumstances, pass by reference semantics are required.

*pass by reference*

Such a capability is not difficult to achieve. If one knows where the variable to be modified is stored in memory, one can simply go to that location and perform the desired operations. Thus, it is possible to change the original object. How does one find out where the object is stored within a function? The address in memory of where the data is stored is passed into the function through a pointer variable.

Let's modify the previous example to work with the original data. Note that when using pass by reference, one does not have to return the modified value. That change is already reflected in the value of the variable as seen in the code module in Figure 7.22. Thus, we save the time to copy the value onto the stack as well as the time to copy the stack value to a local variable in the calling routine.

### EXAMPLE 7.15

```c
#include <stdio.h>
/*

Demonstrate pass by reference in C
*/
void myFunction(int *aValuePtr);

void main(void)
{
    // declare and initialize a working variable
    int myValue = 5;

    // pass the address of the data
    myFunction(&myValue);

    // will show myValue as 9...the original has been changed through the pointer
    printf("main(): myValue is: %d\n", myValue);
    return;
}

void myFunction(int *myValuePtr)
{
    // change the value of the input parameter this change will appear in main
    *myValuePtr = *myValuePtr + 4;

    // will show myValue as 9
    printf("myFunction(): myValue is: %d\n", *myValuePtr);
    return;
}
```

### Figure 7.22 Passing to a Function by Reference

## 7.4.5 Function Name Scope

Without additional qualification, the visibility of the name of a function is restricted to the scope in which it was declared. However, the name of the function declared in one file may be made visible to other files through the qualifier extern, as discussed earlier. Using such a qualifier, one can make the name – the identifier – of the function known to the linker and, thus, make it available for use in other contexts.

There are also times when one wants to restrict the function name from general use. This is what is called information hiding. The C++ and Java languages make widespread use of such capability, although the implementation in those languages is a bit different. In C, one can accomplish information hiding by putting the function name into a separate file and qualifying it with the keyword static as seen in Figure 7.23.

```c
// staticFunc0.c
#include <stdio.h>
// make the function name available
// in this file
extern void myFunc0(void);
// this name will not be available
extern void myFunc1(void);
void main (void)
{
    myFunc0();
    // results in compile error -
    // the function name is not visible
    myFunc1();
    return;
}

// containFunc0.c
#include <stdio.h>
// function prototypes
void myFunc0(void);
// function not visible outside of this file
// ...remove static to make visible
static void myFunc1(void);
// define the functions
void myFunc0(void)
{
    int x = 3;
    printf("x is %d", x);
    return;
}
// remove static to make visible
static void myFunc1(void)
{
    int y = 4;
    printf("y is %d", y);
    return;
}
```

### Figure 7.23 Controlling the Visibility of a Function Name with the Static Qualifier

With such a qualification, the name is not exported – made visible to – the linker. Even with the extern qualifier, the name remains hidden and, thus, is not available for use by other functions, as we saw with static variables.

## 7.4.6 Function Prototypes

In the example program, the line near the top that looks like a function header is called a function prototype; it provides some useful information to the compiler.

```c
// function prototype
int computeArea( int length, int width );
```

Initially, this appears to be duplicate information; it seems that the compiler should be able to get the necessary information from the function header. One problem arises, however. It is uncommon to define a function, that is, provide the header and then provide the actual implementation, later in the program (often in another file), following some other function such a _main()_ that uses it. To ensure that a function call is correct, the compiler examines:

- The expected return type.
- The order, number, and type of arguments provided by the caller.
- The function identifier.

It then tries to match these against the name, signature, and return type for functions that it knows about. If there is no match, the compiler does not know which function body to associate with the call, so it guesses – it is preferable that guessing by the compiler be limited. Such guessing can lead to runtime errors because, without the prototype, the compiler cannot do any type checking.

What happens if a prototype is not provided? If the function is defined before being called, there is no problem. The compiler has sufficient information to perform all of its checks. Otherwise the compiler starts guessing again.

To keep the compiler happy and to enable full-type checking through the prototype, it is sufficient to simply declare the function. The declaration is done by listing the return value (type), the function name, and the function’s signature at the top of the program. In the prototype, it’s only necessary to specify the parameter types; the specific variable names are not necessary.

### Coding Style

Although the variable names are never used by the compiler, they can provide additional information about the intent of each parameter to users of the function.

Good coding style strongly recommends including the names.

Which is more useful as the prototype for computing the area of a rectangle?

```c
int f1(int, int);
```

or

```c
int computeArea(int length, int width);
```

Although both are syntactically correct, the second, using a descriptive function name as well as meaningful parameter names, can significantly improve the readability of a program, mitigate against possible errors, and simplify future enhancements to the function. Often, all of the function prototypes will be placed into a common header file, which can then be included when needed.

The only function that does not require a prototype is _main()_ because there is only one such function in the program. It is the same function prototype in all C programs, so the compiler already knows everything about it.

### Coding Style

When we write a function, we follow the same general guidelines that we did for variables. Always select meaningful and relevant names. Because functions can sometimes be rather complex or may be visible only from their calling interface, good annotation becomes very important. We provide such documentation in a function header.
