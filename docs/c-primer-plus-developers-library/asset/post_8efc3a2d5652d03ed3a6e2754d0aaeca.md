
- It returns a value.
- It requires a prototype.

Consider `stonetolb()` as a standard form for function design. You’ll further explore functions in Chapters 7 and 8. In the meantime, the material in this chapter should give you a good feel for how functions work and how they fit into C++.

## Placing the using Directive in Multifunction Programs

Notice that Listing 2.5 places a `using` directive in each of the two functions:

```cpp
using namespace std;
```

This is because each function uses `cout` and thus needs access to the `cout` definition from the `std` namespace.

There’s another way to make the `std` namespace available to both functions in Listing 2.5, and that’s to place the directive outside and above both functions:

```cpp
// ourfunc1.cpp -- reposition the using directive
#include <iostream>
using namespace std; // affects all function definitions in this file
void simon(int);

int main()
{
    simon(3);
    cout << "Pick an integer: ";
    int count;
    cin >> count;
    simon(count);
    cout << "Done!" << endl;
    return 0;
}

void simon(int n)
{
    cout << "Simon says touch your toes " << n << " times." << endl;
}
```

The current prevalent philosophy is that it’s preferable to be more discriminating and limit access to the `std` namespace to only those functions that need access. For example, in Listing 2.6, only `main()` uses `cout`, so there is no need to make the `std` namespace available to the `stonetolb()` function. Thus, the `using` directive is placed inside the `main()` function only, limiting `std` namespace access to just that function.

In summary, you have several choices for making `std` namespace elements available to a program. Here are some:

- You can place the following above the function definitions in a file, making all the contents of the `std` namespace available to every function in the file:

  `using namespace std;`

- You can place the following in a specific function definition, making all the contents of the `std` namespace available to that specific function:

  `using namespace std;`

- Instead of using `using namespace std;`, you can place using declarations like the following in a specific function definition and make a particular element, such as `cout`, available to that function:

  `using std::cout;`

- You can omit the using directives and declarations entirely and use the `std::` prefix whenever you use elements from the `std` namespace:

  `std::cout << "I'm using cout and endl from the std namespace" << std::endl;`

## Naming Conventions

C++ programmers are blessed (or cursed) with myriad options when naming functions, classes, and variables. Programmers have strong and varied opinions about style, and these often surface as holy wars in public forums. Starting with the same basic idea for a function name, a programmer might select any of the following:

```
MyFunction( )
myfunction( )
myFunction( )
my_function( )
my_funct( )
```

The choice will depend on the development team, the idiosyncrasies of the technologies or libraries used, and the tastes and preferences of the individual programmer. Rest assured that any style consistent with the C++ rules presented in Chapter 3 is correct as far as the C++ language is concerned, and it can be used based on your own judgment.

Language quibbles aside, it is worth noting that a personal naming style—one that aids you through consistency and precision—is well worth pursuing. A precise, recognizable personal naming convention is a hallmark of good software engineering, and it will aid you throughout your programming career.

## Summary

A C++ program consists of one or more modules called functions. Programs begin executing at the beginning of the function called `main()` (all lowercase), so you should always have a function by this name. A function, in turn, consists of a header and a body. The function header tells you what kind of return value, if any, the function produces and what sort of information it expects arguments to pass to it. The function body consists of a series of C++ statements enclosed in paired braces ({}).

C++ statement types include the following:

- **Declaration statement**—A declaration statement announces the name and the type of a variable used in a function.
- **Assignment statement**—An assignment statement uses the assignment operator (=) to assign a value to a variable.
- **Message statement**—A message statement sends a message to an object, initiating some sort of action.
- **Function call**—A function call activates a function. When the called function terminates, the program returns to the statement in the calling function immediately following the function call.
- **Function prototype**—A function prototype declares the return type for a function, along with the number and type of arguments the function expects.
- **Return statement**—A return statement sends a value from a called function back to the calling function.

A class is a user-defined specification for a data type. This specification details how information is to be represented and also the operations that can be performed with the data. An object is an entity created according to a class prescription, just as a simple variable is an entity created according to a data type description.

C++ provides two predefined objects (`cin` and `cout`) for handling input and output. They are examples of the `istream` and `ostream` classes, which are defined in the `iostream` file. These classes view input and output as streams of characters. The insertion operator (`<<`), which is defined for the `ostream` class, lets you insert data into the output stream, and the extraction operator (`>>`), which is defined for the `istream` class, lets you extract information from the input stream. Both `cin` and `cout` are smart objects, capable of automatically converting information from one form to another according to the program context.

C++ can use the extensive set of C library functions. To use a library function, you should include the header file that provides the prototype for the function.

Now that you have an overall view of simple C++ programs, you can go on in the next chapters to fill in details and expand horizons.

## Chapter Review

You can find the answers to the chapter review at the end of each chapter in Appendix J, “Answers to Chapter Review.”

1. What are the modules of C++ programs called?
2. What does the following preprocessor directive do?

   ```cpp
   #include <iostream>
   ```

3. What does the following statement do?

   ```cpp
   using namespace std;
   ```

4. What statement would you use to print the phrase “Hello, world” and then start a new line?
5. What statement would you use to create an integer variable with the name cheeses?
6. What statement would you use to assign the value 32 to the variable cheeses?
7. What statement would you use to read a value from keyboard input into the variable cheeses?
8. What statement would you use to print “We have X varieties of cheese,” where the current value of the cheeses variable replaces x?
9. What do the following function prototypes tell you about the functions?

   ```cpp
   int frop(double t);
   void rattle(int n);
   int prune(void);
   ```

10. When do you not have to use the keyword `return` when you define a function?
11. Suppose your `main()` function has the following line:

    ```cpp
    cout << "Please enter your PIN: ";
    ```

    And suppose the compiler complains that `cout` is an unknown identifier. What is the likely cause of this complaint, and what are three ways to fix the problem?

## Programming Exercises

1. Write a C++ program that displays your name and address (or if you value your privacy, a fictitious name and address).
2. Write a C++ program that asks for a distance in furlongs and converts it to yards. (One furlong is 220 yards.)
