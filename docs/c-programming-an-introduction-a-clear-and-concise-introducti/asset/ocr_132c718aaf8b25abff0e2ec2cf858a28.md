Running the program again, we get the following output:

```
banana apple
apple banana
banana apple
```

So the values are switched inside the function but revert back to the original values after the function call.

The reasons our values aren’t being switched is due to a rule of parameter passing in C++. This rule states that by default, the parameters to a function are passed by value from the calling program to the function. The phrase “by value” means that when a function is called, the C++ compiler makes a copy of the parameter values and passes that copy to the calling program. When the function is complete and control returns to the program, the values of the parameters are removed from memory, even if they have been changed, as in the swap() function example above, and the variables in the program retain their original values (they never actually lost their value as copies were made for use by the function parameters).

If we want a calling function to be able to permanently change the function parameters, we have to pass the parameters by reference. Passing “by reference” means that the compiler is, in effect, passing the actual parameter to the function, so that the function can access and change the value of the parameter such that it will retain its new value when control is passed back to the calling program.

To pass a parameter by reference, place an ampersand (&) before the parameter name. The ampersand is called the reference operator. We’ll discuss it more later in the book.

Here is an example of a function definition for a function that adds 5 to the parameter passed to it: