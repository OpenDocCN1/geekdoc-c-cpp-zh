```
char * reverse(char * str, int n)
{
   char t;
   if((*str == '\0') || (str > (str + n - 1)))
      return str;
   t = (*str + n - 1);
   *(str + n - 1) = *str;
   *str = t;
   reverse(str + 1, n-2);
   return str;
}
```

> The program displays the following output
> Enter the string : Software
> Its reversal is ErawftOFS

# 2.14 Summary

+   A function is a self-contained program segment that performs some specific well defined task.

+   Three steps in using a function are declaring a function, defining a function and calling the function.

+   A function is called by specifying its name, followed by a pair of parenthesis which contains parameters if needed.

+   The argument that represents the names of data items that are transformed into the function from the calling portion of the program are called as formal arguments or formal parameters.

+   The corresponding arguments in the function reference which define the data items that are actually transferred are called as actual arguments or actual parameters.

+   The return statement is used to return the information from the function to the calling function of the program.

+   A function may be declared anywhere as long as its declaration is above all references to the function. So, a function should be declared before it is called.

+   The execution of a function is terminated when it executes the return statement or when the last statement of the function is executed or when it encounters the closing brace of the function.

+   A function prototype declares the return type of the function and declares the number type and the sequence of the parameters that a function will receive.

+   Recursion is a process by which a function calls itself repeatedly until some specified condition has been satisfied.

+   Scope of a variable has been defined as the region over which the variable is visible or valid. Scope is usually established by a set of flower braces.