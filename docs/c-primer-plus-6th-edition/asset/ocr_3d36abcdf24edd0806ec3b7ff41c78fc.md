# Using Library Functions

C++ library functions are stored in library files. When you compile a program, it must search the library files for the functions you've used. Compilers differ on which library files they search automatically. If you try to run Listing 2.4 and get a message that _sqrt is an undefined external (sounds like a condition to avoid!), chances are that your compiler doesn't assign an underscore prefix to function names—another subtle reminder that they have last say about your program.) If you get a message, check your compiler documentation to see how to have your compiler search the correct library. If you get such a complaint on a Unix implementation, for example, it may require that you use the -lm option at the end of the command line:

```
CC sqrt.C -lm
```

Some versions of the Gnu compiler under Linux behave similarly:

```
++ sqrt.C -lm
```

Merely using the cmath header file provides the prototype but does not necessarily cause the compiler to search the correct library file.

Here's a sample run of the program in Listing 2.4:

Enter the floor area, in square feet, of your home: 1536
That's the equivalent of a square 39.1918 feet to the side.
How fascinating!

Because sqrt() works with type double values, the example makes the variables type. Note that when you declare a type double variable by using the same form, or syntax, as when you declare a type int variable:

```
type-name variable-name;
```

Type double allows the variables area and side to hold values with decimal fractions, such as 1536.0 and 39.1918. An apparent integer, such as 1536, is stored as a real value with a decimal fraction of .0 when stored in a double variable. As you'll see in Chapter 3, type double encompasses a much greater range of values than type int.

C++ allows you to declare new variables anywhere in a program, so sqrt.cpp didn't declare side until before using it. C++ also allows you to assign a value to a .var when you create it, so you could also do this:

```
double side = sqrt (area);
```

You'll learn more about this process, called initialization, in Chapter 3.

Note that cin knows how to convert information from the input stream to type double, and cout knows how to insert type double into the output stream. As noted earlier, these objects are smart.