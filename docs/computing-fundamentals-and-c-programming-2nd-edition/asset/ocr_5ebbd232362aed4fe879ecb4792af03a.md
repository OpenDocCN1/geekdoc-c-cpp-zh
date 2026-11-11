# ## 11.5 DEFINITION OF FUNCTIONS

A *function definition*, also known as *function implementation* shall include the following elements:

+   1. function name;
+   2. function type;
+   3. list of parameters;
+   4. local variable declarations;
+   5. function statements; and
+   6. a return statement.

All the six elements are grouped into two parts, namely,

+   - function header (First three elements); and
+   - function body (Second three elements).

A general format of a function definition to implement these two parts is given below:

```
```
function_type function_name(parameter list)
{
    local variable declaration;
    executable statement1;
    executable statement2;
    . . . . .
    . . . . .
    return statement;
}
```
```

The first line *function_type function_name(parameter list)* is known as the *function header* and the statements within the *opening and closing braces* constitute the *function body*, which is a compound statement.

# ### 11.5.1 Function Header

The function header consists of three parts: the function type (also known as *return type*), the function name, and the *formal* parameter list. Note that a semicolon is not used at the end of the function header.

# ### 11.5.2 Name and Type

The *function type* specifies the type of value (like *float* or *double*) that the function is expected to return to the program calling the function. If the return type is not explicitly specified, C will assume that it is an integer type. If the function is not returning anything, then we need to specify the return type as *void*. Remember, *void* is one of the fundamental data types in C. It is a good programming practice to code explicitly the return type, even when it is an integer. The value returned is the output produced by the function.

The *function name* is any valid C identifier and therefore must follow the same rules of formation as other variable names in C. The name should be appropriate to the task performed by the function. However, care must be exercised to avoid duplicating library routine names or operating system commands.