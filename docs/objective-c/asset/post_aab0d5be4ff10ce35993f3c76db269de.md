
The return value type is specified to the left of the function name. The return value does not have a variable name associated with it as part of the declaration. You define what value is returned from your function by using the return keyword inside your function body. This should be the last statement of your function.

In Objective-C, parameters and return values are passed using what’s called “pass by value.” What this means is that when you pass a parameter to a function, the runtime will actually make a copy of the value that you are passing. This means that changes made to those values inside of your function will not affect the value in the calling function. If, however, you pass a pointer to your value instead, then changes made to the dereferenced variable will be sent back to the original variable in the calling function.

Listing 2.26 demonstrates this concept.

## Listing 2.26
### Working with pointers
```
#import <Foundation/Foundation.h>

void myFunction(int a, int *b)
{
    a = 20;
    *b = 20; // de-reference the pointer to access the original
}

int main(int argc, const char *argv[])
{
    int a = 10;
    int b = 10;

    myFunction(a, &b); // using the & operator changes b into a pointer

    NSLog(@"a: %ld", a);
    NSLog(@"b: %ld", b);

    return 0;
}
```

Similarly, when returning values from functions, you have to be careful to not return pointers or references to variables that will be out of scope when the function exits. For example, if you return the address of a value inside of your function, when the calling function tries to access that value, that variable will have been deallocated and therefore will no longer be available — this causes a crash.

When I talk about objects in Chapter 3 and memory management in Chapter 4, I will show you how you can return pointers created in your functions to other functions. For now, however, stick with simple values.

## Understanding implementation versus interface

Collections of functions can be grouped together into separate source files so that you don’t have to clutter your main source with all your programming logic. These source files are typically called units.

When you separate your source code into units, a unit consists of two files: One of them contains declarations of your functions, the other one contains definitions for those declarations. Understanding the difference between declarations and definitions is an important concept that you need to understand.

You’ve already seen function definitions. The functions that you’ve worked with so far have all been fully defined. A function definition is where you actually write the code that makes up the function itself. A function declaration declares the function signature for your function including the return type, the function name, and its parameters. It does not include the actual definition of what the function does.

Function declarations can be said to be declaring the interface to your function. This is a loose definition, but later, when we discuss object-oriented programs, you will see that this concept of interfaces is heavily used.

Extending this idea, the function definition can therefore be said to be the implementation of the interface that you declared.

To declare a function that can be used in other units, you use the extern keyword and then the function signature just like your function definition. Because a function declaration is a statement, just like declaring a variable, you also need to include an additional semicolon at the end of your function signature. Knowing when to place the semicolon and when not to is a common mistake new programmers make. Be sure to remember that the semicolon comes after the declaration but not after the definition.

So, imagine that we wanted to encapsulate our factorial calculation method in its own unit.

To do so would take three steps. The first step would be to create the interface file for our unit. Typically, interface files in Objective-C use a .h extension, which stands for “Header.” Create a new Header file in your Xcode project called “Factorial.h” and add to it the code in Listing 2.27.

## Listing 2.27
### Function declaration
```
extern long int calculateFactorial(int value);
```

This is the function declaration for the calculateFactorial function. The next step is to create an implementation file. The implementation file has as .c extension. Create a new C source file in your Xcode project called “Factorial.c” and modify it to look like Listing 2.28.

## Listing 2.28
### Function definition
```
long int calculateFactorial(int value)
{
    long int result = 1;

    for(int i = 1; i <= value; ++i)
    {
        result = result * i;
    }

    return result;
}
```

Finally, you have to modify the file that calls your function to include the interface file for your unit. Modify your own source file to look like Listing 2.29.

## Listing 2.29
### Calling the function
```
#import <Foundation/Foundation.h>
#import "Factorial.h"

int main (int argc, const char * argv[])
{
NSLog(@"5!: %ld", calculateFactorial(5));
NSLog(@"10!: %ld", calculateFactorial(10));
NSLog(@"15!: %ld", calculateFactorial(15));
NSLog(@"20!: %ld", calculateFactorial(20));

return 0;
}
```

The definition of the function is now removed from this file and replaced with an import command.

Import statements are used to include other units’ interfaces in your current unit. The import statement works by searching through the directories of your project and through the frameworks associated with your project for the interface file that you want to include. When you use angle brackets <> to enclose the filename, as in the case with the Foundation framework, it searches the system paths for the interface file. When you use quotes, the statement only searches the current directory of your project and any of its subdirectories.

The rules concerning the search directories for interface files can be difficult to remember, so I suggest you simply remember these two rules of thumb: If an interface file is part of your project, and something that you created, then you want to use quotes when specifying it in an import statement; otherwise, if the interface file is part of a third-party framework or part of the frameworks provided by Apple, then you want to use angle brackets.

## Linking with implementation files

After you split your code into units and use those units in your code, you still have one more thing that you need to do. You need to ensure that the implementation file is linked to your executable. An executable is made up of multiple implementation files linked together with the Objective-C runtime. As you add more implementation files to your project, you have to make sure that they are also linked with your executable. Typically, when you create a new file, Xcode asks you if you want to include it in your project. In Figure 2.6, notice the check box indicating that this file will be added to the Listing 2.6 target.

If, however, you forget to do so, or if you add another target and need to include an existing implementation file in that target as well, then it’s important for you to also know how to manually link an existing implementation file with your current target.

To do so, simply select the implementation file that you want to include in your current target, click on the Detail tab above the editor, and ensure that the check box under the bull’s-eye column is selected, as shown in Figure 2.7.

Again, notice the bull’s-eye check box, which is unchecked for our “NewFile.m” file. To include this file in your current target, select this check box.

Now that you know some of the basics of syntax and program organization, take a look at how you can control flow in an Objective-C program.

## Figure 2.6
Adding a file to your target

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_78_0.png)

## Figure 2.7 The target check box

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_79_0.png)

## Controlling Program Flow

Applications would be pretty dull if they could only do one thing. If you couldn't have them branch and make decisions based on conditions at runtime, they wouldn't be very useful. Fortunately, we don't have to worry about that, because Objective-C provides us with a rich toolkit of flow control mechanisms.

These flow control mechanisms fall under two broad categories.

The mechanisms in the first category, conditional statements, enable you to change the execution path of your application based on runtime conditions. You can have a fork in the road, essentially, in the middle of your application. Which path your application takes can be determined based on the variables. Those variables can be set based on the parameters, user input, or any other condition that you want.

The second category of flow control mechanisms is that of loops. Loops enable you to perform some set of operations repeatedly until some condition is met. This enables you to do things like iterating over items in a list, doing something for some set number of times, and so on.
