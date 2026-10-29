3. A function’s return type is the data type of the value the function returns. If no type is declared, the function is assumed to return an integer value. If the function doesn’t return a value, it should be declared as a void type.

4. Functions can return at most a single data type value to their calling functions. This value is the value of the expression in the return statement.

5. Arguments passed to a function, when it’s called, must conform to the parameters specified by the function header in terms of order, number of arguments, and specified data type.

6. Using reference parameters, a variable’s address is passed to a function. If a called function is passed an address, it has the capability to access the calling function’s variable. Using passed addresses permits a called function to return multiple values.

7. Functions can be declared to all calling functions by means of a function prototype. The prototype provides a declaration for a function that specifies the data type the function returns, the function’s name, and the data types of arguments the function expects. As with all declarations, a function prototype is terminated with a semicolon and can be included in local variable declarations or as a global declaration. This is the most common form of a function prototype:

```
`dataType functionName(parameter data type list);`
```

If the called function is placed above the calling function in the program, no further declaration is required because the function’s definition serves as a global declaration to all subsequent functions.

8. Every variable in a program has a scope, which determines where in the program the variable can be used. A variable’s scope is local or global and is determined by where the variable’s definition statement is placed. A local variable is defined in a function and can be used only in its defining function or block. A global variable is defined outside a function and can be used in any function following the variable’s definition. All global variables that aren’t specifically initialized by the user are initialized to 0 by the compiler, and global variables not declared as static can be shared between files by using the keyword extern.

9. Every variable also has a storage category, which determines how long the value in the variable is retained, also known as the variable’s lifetime. Auto variables are local variables that exist only while their defining function is executing; register variables are similar to auto variables but are stored in a computer’s registers rather than in memory; and static variables can be global or local and retain their values while the program is running. All static variables are set to 0 when they’re defined if the user doesn’t initialize them explicitly.