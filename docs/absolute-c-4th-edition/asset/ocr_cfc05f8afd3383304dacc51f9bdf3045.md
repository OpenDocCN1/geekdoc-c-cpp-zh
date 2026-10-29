Now suppose your program also requires a function to compute the average of three numbers. You might define a new function called ave3 as follows:

```
```cpp
double ave3(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```
```

This will work, and in many programming languages you have no choice but to do something like this. However, C++ overloading allows for a more elegant solution. In C++ you can simply use the same function name ave for both functions. In C++ you can use the following function definition in place of the function definition above:

```
```cpp
double ave(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```
```

so that the function name ave then has two definitions. This is an example of overloading. In this case we have overloaded the function name ave. Display 4.6 embeds these two function definitions for ave into a complete sample program. Be sure to notice that each function definition has its own declaration (prototype).

The compiler can tell which function definition to use by checking the number and types of the arguments in a function call. In the program in Display 4.6, one of the functions called ave has two arguments and the other has three arguments. When there are two arguments in a function call, the first definition applies. When there are three arguments in a function call, the second definition applies.

# OVERLOADING A FUNCTION NAME

> If you have two or more function definitions for the same function name, that is called *overloading*. When you overload a function name, the function definitions must have different numbers of formal parameters or some formal parameters of different types. When there is a function call, the compiler uses the function definition whose number of formal parameters and types of formal parameters match the arguments in the function call.

Whenever you give two or more definitions to the same function name, the various function definitions must have different specifications for their arguments; that is, any two function definitions that have the same function name must use different numbers of formal parameters or have one or more parameters of different types (or both). Note that when you overload a function name, the declarations for the two different definitions must differ in their formal parameters. *You cannot overload a function name by giving two definitions that differ only in the type of the value returned.* Nor can you