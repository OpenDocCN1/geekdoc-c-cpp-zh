# 9.2. USING FUNCTIONS

n within prompt is bound to 2.

> A function's definition requires that all formal parameters be declared in the parentheses following the function's name. A caller does not provide actual parameter declarations when calling the function. Given the square_root function defined in Listing 9.1 (customsquareroot.cpp), the following caller code fragment is illegal:

```
double number = 25.0;
// Pass the variable's value to the function
cout << square_root(number) << endl;
// Illegal, do not declare the parameter during the call
cout << square_root(double number) << endl;
```

The function definition is responsible for declaring the types of its parameters, not the caller.

# 9.2 Using Functions

The general form of a function definition is

```
type name ( parameterlist )
{
  body
}
```

+   * The type of the function indicates the type of value the function returns. Often a function will perform a calculation and the result of the calculation must be communicated back to the place where the function was invoked. The special type void indicates that the function does not return a value.
* The name of the function is an identifier (see Section 3.3). The function's name should indicate the purpose of the function.
* The parameterlist is a comma separated list of pairs of the

type name
where type is a C++ type and name is an identifier representing a parameter. The caller of the function communicates information into the function via parameters. The parameters specified in the parameter list of a function are called formal parameters. A parameter is also known as an argument. The parameter list may be empty; empty parameter list indicates that no information may be passed into the function caller.

+   * The body is the sequence of statements, enclosed within curly braces, that define the actions that the function is to perform. The statements may include variable declarations, and any variables declared within the body are local to that functionnThe body may contain only one statement, many statements, or nothing at all; regardless, the curly braces always are required.