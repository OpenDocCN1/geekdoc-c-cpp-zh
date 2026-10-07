# 382 Chapter 8 Adventures in Functions

```
using namespace std;
double a, b;
double c = 13.0;

a = square(5.0);
b = square(4.5 + 7.5); // can pass expressions
cout << "a = " << a << ", b = " << b << "\n";
cout << "c = " << c << "\n";
cout << ", squared = " << square(c++) << "\n";
cout << "Now c = " << c << "\n";
return 0;
```

Here's the output of the program in Listing 8.1:

```
a = 25, b = 144
c = 13, squared = 169
Now c = 14
```

This output illustrates that inline functions pass arguments by value just like regular functions. If the argument is an expression, the function passes the value of the expression—12 in this case. C++'s inline facility is far superior to C macro definitions. See the "Inline Versus Macros" sidebar.
Even though the program doesn't provide a separate prototype, C++'s prototyping features are still in play. That's the entire definition, which comes before the function's first use, serves as a prototype. This means you can use square() with an int or long argument, and the program automatically casts the type double before passing it to the function.

# Inline Versus Macros

The inline facility is an addition to C++. C uses the preprocessor #define statement to provide macros, which are crude implementations of inline code. For example, here's a macro for squaring a number:

```
#define SQUARE(X) X*X
```

This works by passing arguments but through text substitution, with the x acting as a symbolic label for the "argument":

```
a = SQUARE(5.0); is replaced by a = 5.0*5.0;
b = SQUARE(4.5 + 7.5); is replaced by b = 4.5 * 4.5 + 7.5 * 7.5;
d = SQUARE(c++); is replaced by d = c++*c++
```

Only the first example works properly. You can improve matters with a liberal application of parentheses:

```
#define SQUARE(X) ((X)*(X))
```