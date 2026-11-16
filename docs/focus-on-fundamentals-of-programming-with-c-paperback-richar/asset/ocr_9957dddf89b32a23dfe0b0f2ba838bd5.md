# **Function Call 2:**

Values are assigned to variables `l` and `w` and the variables are the arguments to the function `calcRectArea()`. The function returns a calculated value that is assigned to `area`, which is then output.

Note that in this case the names of the arguments that are passed to the function (called the *actual parameters*) do not have the same name as the arguments that are received by the function (called the *formal parameters*). The names do not need to match! C simply passes the first actual parameter to the first formal parameter, the second actual parameter to the second formal parameter, etc.

However, the number of actual parameters must equal the number of formal parameters (i.e., the number of parameters that are passed to a function must be the same as the number of parameters that the function is declared to receive). Additionally, the data type of the first actual parameter must match the data type of the first formal parameter, the data type of the second actual parameter must match the data type of the second formal parameter, etc.

# **Function Call 3:**

The function return value is not assigned to a variable for output as the function call is itself included within the `printf()` statement! Here the return `int` value is substituted into the `printf()` string for the `%d` format specifier and the return value of the function is immediately output.

# **Function Call 4:**

This function call, while technically correct, does not use the value returned by the function because we're calling the function without assigning or using the return value in any way. The returned value is simply ignored! We'll see other examples of function calls in which the returned value goes unused.

# **Function Advantages**

+   • Programs become more readable.

+   • Function can be tested and debugged separately from the rest of the program.

+   • By isolating a logic step in a function, the parts of a program are more independent and the likelihood of errors are reduced.

+   • The same function can be invoked from different places in a program. Therefore, a commonly used chunk of logic needs to be written only once.