```
void cdabs(float x) // compute and display absolute value of a float
{
    if ( x < 0 )
        x = -x;
    cout << "The absolute value of the float is " << x << endl;
}
```

```
void cdabs(double x) // compute and display absolute value of a double
{
    if ( x < 0 )
        x = -x;
    cout << "The absolute value of the double is " << x << endl;
}
```

Which of the three cdabs() functions is actually called depends on the argument types supplied at the time of the call. Therefore, the function call cdabs(10); causes the compiler to use the function named cdabs() that expects an integer argument, and the function call cdabs(6.28f); causes the compiler to use the function named cdabs() that expects a double-precision argument.⁶

Notice that overloading a function’s name simply means using the same name for more than one function. Each function that uses the name must still be written and exists as a separate entity. The use of the same function name doesn’t require code in the functions to be similar, although good programming practice dictates that functions with the same name should perform essentially the same operations. All that’s required to use the same function name is ensuring that the compiler can distinguish which function to select, based on the data types of the arguments when the function is called. Clearly, however, if the only difference in the overloaded functions is the argument types, a better programming solution is simply creating a function template, discussed in the next section. Using overloaded functions, however, is extremely useful with constructor functions, explained in Section 10.3.

# Function Templates⁷

In most high-level languages, including C++’s immediate predecessor, C, each function must be coded separately, even if function overloading is used to give multiple functions the same name. For example, consider determining and displaying a number’s absolute value. If the number passed to the function can be an integer, a single-precision, or a double-precision