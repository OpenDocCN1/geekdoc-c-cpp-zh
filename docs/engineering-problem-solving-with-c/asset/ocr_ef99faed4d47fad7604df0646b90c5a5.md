check all future references to sinc() to insure that the reference is compatible with the function prototype. Note that the compiler does not need the identifier x to check future references to sinc(). In fact, the following function prototype statement is also valid for program chapter 6_3.

```
double sinc(double);
```

Both of these function prototypes provide the same information to the compiler. We recommend using identifiers in function prototypes because the identifiers help document the order and definition of the parameters.

> **Statement Box 6.2**
> Function Prototype Statements: A function prototype provides information to the compiler to allow the compiler to detect potential errors when a function is referenced.
> 
> Syntax:
> return-type function name(parameter list);
> 
> Examples:
> Prototype:
> double sinc(double x);
> Valid references:
> double y(-5);
> cout << sinc(y);
> cout << sinc(1.5);
> cout << sinc(10);
> y = sinc(0.0);
> Invalid reference:
> sinc("1.5 *");
> sinc(10');
> ERROR MESSAGE:
> Invalid string argument, expected double
> Invalid char argument, expected double
> 
> Prototype:
> void clearScreen(ostream&);
> Valid reference:
> clearScreen(cout);
> Invalid reference:
> cout<<clearScreen(cout);
> ERROR MESSAGE
> std::operator<<error, clearScreen() is a void function

Function prototypes should be included at the top of a program file, outside of any statement block, in order to make the function prototypes available to all functions defined within the file. In other words, including function prototypes at the top of the program file, outside all statement blocks, gives the function prototypes file scope or global scope. Scope will be discussed in more detail in the following section. Header files, such as cmath, contain function prototypes for the functions included in the header files; otherwise, we would need to include individual prototypes for functions such as log() and sqrt() in our programs.

If a program references a large number of programmer-defined functions, it becomes cumbersome to include all the function prototype statements. In these cases, a custom header

file scope
global scope

custom header file