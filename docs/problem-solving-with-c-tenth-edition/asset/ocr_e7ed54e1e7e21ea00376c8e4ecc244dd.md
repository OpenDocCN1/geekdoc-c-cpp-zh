declarations and executable statements in a function definition are the same as they are for the main part of a program. However, unless you have reason to do otherwise, it is best to place the declarations first, as indicated in Display 4.6.

Since a function does not return a value until it executes a return statement, a function must contain one or more return statements in the body of the function. A function definition may contain more than one return statement. For example, the body of the code might contain an if-else statement, and each branch of the if-else statement might contain a different return statement, as illustrated in Display 4.5.

Any reasonable pattern of spaces and line breaks in a function definition will be accepted by the compiler. However, you should use the same rules for indenting and laying out a function definition as you use for the main part of a program. In particular, notice the placement of braces {} in our function definitions and in Display 4.6. The opening and closing braces that mark the ends of the function body are each placed on a line by themselves. This sets off the function body.

Spacing and line breaks

# More About Placement of Function Definitions

We have discussed where function definitions and function declarations are normally placed. Under normal circumstances these are the best locations for the function declarations and function definitions. However, the compiler will accept programs with the function definitions and function declarations

# DISPLAY 4.6 Syntax for a Function That Returns a Value

```
Function Declaration

Type_Returned Function_Name(Parameter_List);
Function_Declaration_Comment

Function Definition

Type_Returned Function_Name(Parameter_List) ← function header
{
    Declaration_1
    Declaration_2
    ...
    Declaration_Last
    Executable_Statement_1
    Executable_Statement_2
    ...
    Executable_Statement_Last
}
body
Must include one or more return statements.
```