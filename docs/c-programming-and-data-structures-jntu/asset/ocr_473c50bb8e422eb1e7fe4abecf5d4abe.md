# 10.14 C Programming and Data Structures

While the formal arguments must be valid variable names, the actual arguments may be variable names, expressions, or constants. The variables used in actual arguments must be assigned values before the function call is made.

Remember that, when a function call is made, only a copy of the values of actual arguments is passed into the called function. What occurs inside the function will have no effect on the variables used in the actual argument list.

# Example 10.2

Modify the program of Example 10.1 to include the arguments in the function calls.

The modified program with function arguments is presented in Fig. 10.7. Most of the program is identical to the program in Fig. 10.4. The input prompt and scanf assignment statement have been moved from value function to main. The variables principal, inrate, and period are declared in main because they are used in main to receive data.

value(principal, inrate, period); passes information it contains to the function value.

The function header of value has three formal arguments p, r, and n which correspond to the actual arguments in the function call, namely, principal, inrate, and period. The formal arguments are declared immediately after the function header. On execution of the function call, the values of the actual arguments are assigned to the corresponding formal arguments. In fact, the following assignments are accomplished across the function boundaries:

p = principal; r = inrate; n = period;

The variables declared inside a function are known as local variables and therefore their values are local to the function and cannot be accessed by any other function. We shall discuss more about this later in the chapter.

The function value calculates the final amount for a given period and prints the results as before. Control is transferred back on reaching the closing brace of the function. Note that the function does not return any value.

The function printline is called twice. The first call passes the character 'Z', while the second passes the character 'C' to the function. These are assigned to the formal argument ch for printing lines (see the output).

# 10.10 ARGUMENTS WITH RETURN VALUES

The function value in Fig. 10.7 receives data from the calling function through arguments, but does not send back any value. Rather, it displays the results of calculations at the terminal.

```
Program
p
FUNCTIONS WITH ARGUMENTS BUT NO RETURN VALUES
main()
{
```

```
p
FUNCTIONS WITH ARGUMENTS BUT NO RETURN VALUES
main()
{
```