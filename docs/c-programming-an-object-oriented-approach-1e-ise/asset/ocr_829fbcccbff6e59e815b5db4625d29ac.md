# EXAMPLE 6.3

The following shows how we can call our larger function in *main* as many times as we want.

```
```cpp
int main ()
{
   cout << larger (3, 13);
   cout << larger (10, 12);
   cout << larger (2, 12);
   return 0;
}
```
```

You may have noticed that the *main* function we used in previous chapters is itself the definition of a function. The function is called by the C++ run-time environment. Its header tells us that it returns an integer, but its parameter list is empty (Appendix N shows the *main* function with a parameter list).

# Arguments and Parameters

Before we close this section, we discuss two terms used in functions: arguments and parameters. A *parameter* is a variable declared in the header of the function definition; an *argument* is a value that initializes the parameter when the function is called. In other words, a parameter is like a variable on the left-hand side of an assignment statement; the corresponding argument is like the value used on the right-hand side of the assignment statement. The initialization of the parameter is done explicitly by the system when a function is called.

The following shows the function call with the assignment statement. The parameter *x* is initialized with argument 5.

```
```cpp
int main ()
{
   ...
   fun (5);          // Function call; 5 is an argument
   ...
}
void fun (int x)     // Function definition; x is a parameter
{
   ...
}
```
```

As we will see, the argument can be a variable or even an object, but only its value takes part in the function call.

# 6.1.3 Library and User-Defined Functions

To use functions in a program, we must have a function definition and a function call. However, we must choose between two types: library functions and user-defined functions.

# Library Functions

The C++ library contains predefined functions. We need only the declaration of the functions to call them. We study some of these functions later in this chapter.