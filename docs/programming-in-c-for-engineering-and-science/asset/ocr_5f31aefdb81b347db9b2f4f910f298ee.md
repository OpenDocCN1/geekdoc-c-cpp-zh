# 10.6 INLINING, OVERLOADING, AND TEMPLATES

In this section we will consider three additional properties of functions:

+   1. Inlining: In applications where function calls and returns are too time-consuming, inlining can be used to improve speed of execution.
+   2. Overloading: Functions may have the same name, provided the compiler is able to distinguish between them; this is known as overloading the functions.
+   3. Templates: A function template is a pattern for a function that can be used to generate a collection of functions that have the same name but process different kinds of data.

# 10.6.1 Inline Functions

We have seen that when one function f() calls another function g(), execution is transferred from f() to g(). When g() terminates, a second transfer of control is necessary to return execution back to f(). Each function call significantly increases the amount of time required for a program to execute—a considerable amount of time in fact, compared to the speed at which a computer normally operates. In many situations, the overhead associated with function calls is acceptable, but there are other occasions in which execution time is so important that this overhead cannot be tolerated. For these problems, C++ provides inlining of functions.

One of the details we have omitted (for simplicity) in the discussion of functions is that a definition can be preceded by a function specifier, which provides the compiler with special instructions about the function:

```
specifier return_type function_name(parameter_declaration_list)
{
    statement_list
}
```

One such specifier is the inline specifier that instructs the compiler to use the C++ inline mechanism to avoid the overhead of normal function calls.

To illustrate, suppose we want to inline the temperature-conversion function celsiusToFahrenheit() from Section 6.2. We can do so by preceding its prototype and its definition with the inline specifier:

```
inline double celsiusToFahrenheit(double tempCelsius);
.
.
.
inline double celsiusToFahrenheit(double tempCelsius)
{
    return 1.8 * tempCelsius + 32;
}
```