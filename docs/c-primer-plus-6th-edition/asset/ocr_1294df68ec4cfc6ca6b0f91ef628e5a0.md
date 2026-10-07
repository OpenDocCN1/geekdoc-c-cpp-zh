# Function Review 311

But I said earlier that you should concentrate on the prototypes. What should you know about prototypes? First, you should understand why C++ requires prototypes. Then because C++ requires prototypes, you should know the proper syntax. Finally, you should appreciate what the prototype does for. Let's look at these points in turn, using Listing 7.2 as a basis for discussion.

# Why Prototypes?

A prototype describes the function interface to the compiler. That is, it tells the compiler what type of return value, if any, the function has, and it tells the compiler the number and type of function arguments. Consider how the prototype affects this function call from Listing 7.2:

```
double volume = cube(side);
```

+   First, the prototype tells the compiler that cube() should have one type double argument. If the program fails to provide the argument, prototyping allows the compiler to catch the error. Second, when the cube() finishes its calculation, it places its return value at some specified location—perhaps in a CPU register, perhaps in memory. Then when calling, main() in this case, it retrieves the value from location. Because the prototype states that cube() is type double, the compiler knows how many bytes to retrieve and how to interpret them. Without that information, the compiler could only guess, and that is something compilers won't.
Still much, why does the compiler need a prototype? Can't it just look further in the file and see how the functions are defined? One problem with that approach is it not very efficient. The compiler would have to put compiling main() on hold while searching the rest of the file. An even more serious problem is the fact that the function might not even be in the file. C++ allows you to spread a program over several files, which you can compile independently and then combine later. In such a case, the compiler might not have access to the function code when it's compiling main().Same is true if the function is part of a library.The only way to avoid using a prototype is to place the function definition before its first use. That is not always possible. Also the C++ programming style is to put main() first because it generally provides the structure for the whole program.

# Prototype Syntax

A function prototype is a statement, so it must have a terminating semicolon. The simplest way to get a prototype is to copy the function header from the function definition and add a semicolon.That's the program in Listing 7.2 for cube():

```
double cube(double x); // add; // header to get prototype
```