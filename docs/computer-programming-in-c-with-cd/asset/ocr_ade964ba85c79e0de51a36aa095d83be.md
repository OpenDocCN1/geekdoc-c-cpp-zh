What are namespaces all about? When you write your own programs, you define your own objects, and when you combine your work with the code written by other people, the names of those objects may conflict with the names that have already been used by other people. In order to avoid this confusion, C++ allows you specify a namespace to define the objects of your program. For this purpose, the ANSI/ISO committee decided to use namespaces as a standard part of C++, and all items declared in the iostream header file are part of the std namespace.

Next, in Listing 2, there is a C++ *comment*, which is an annotation that is added to the C++ code to make the code more readable. You use comments to annotate your code for your own purposes or to make it easier for others to understand what is going on in the program. In Listing 2, the comment explains the working of the program. As far as C++ is concerned, everything on a line following `//` is ignored by the compiler; the view of Listing 2 that a compiler interprets is as follows:

```
```cpp
#include <iostream.h>
int main ()
{
    cout << "Hello from C++." << endl;
    return 0;
}
```
```

> We learn more about comments in the Comments section ahead in this chapter.

After inserting a comment in Listing 2, comes a significant function named `main()`.
You are probably familiar with the idea of functions; they are the basic building blocks of programming. The `main()` function is known as the entry point in a C++ program because this function is invoked by the operating system when you run the program. This simply means that the code included in the `main()` function executes first. We introduced the `int` keyword just before the `main()` function, which indicates that the `main()` function will return an integer value to the operating system.

Next in Listing 2, you see the code of the program, which is enclosed in the curly braces, `{ }`.

When the program executes, the `Hello from C++.` message is displayed. C++ uses the `iostream` object named `cout` to display text. The `cout` object handles the text-based output you want to display from a program.

> The `cout` object will be discussed in detail in Chapter 2, *Working with Input/Output and Flow Control*.

In Listing 2, we use the `<<` *operator* to send the text, Hello from C++ to the `cout` object. You are familiar with the idea of operators; you use operators to perform work on data values called *operands* (for example, 2+3 uses the + operator to add the operands 2 and 3). In the C language, the `<<` operator is used as the left-shift operator, but in C++