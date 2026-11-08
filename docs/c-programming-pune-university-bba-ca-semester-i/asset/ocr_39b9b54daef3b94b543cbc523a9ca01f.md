# ### 6.1.2 Function Definition

+   1. Function Definition is a body of the function written outside the main function.
+   2. The function Definition has a function header statement with a body of statements enclosed within { and }
+   3. Function definition has two main components (1) First Line Function Header (2) Body of function enclosed with { }
+   4. The First Header statement Consists of type specification of the value returned by the function followed by function name and followed by ( )
+   5. Within ( ) round brackets either can be empty or it can have parameters or arguments with data type of each argument

**The Syntax of function definition is:**

```
    return_type function name (no. of parameters/arguments with data types)
    {
        c statement;   // Block code of statements //
        c statement;
        return statement;
    }
```

**Return_type:** Every function returns a value after execution of block of statements, Return type can be of any data type such as int, double, char, void, short, etc.. Normally, function return type is any datatype but if function does not return any value then we have to specify with void keyword to indicate function returns null value.

**Function_name:** Function name should be valid identifier and function name should be a meaningful name so that it can be easy to understand the purpose of function just by seeing it's name.

**Argument list/parameter list (type arg1, type arg2):** Arguments are also called parameters, parameter list contains variables names along with their data types. These arguments are positional formal/dummy parameters whose value can be replaced with actual parameter during function call. For example – A function which is used to add three integer variables, will have three integer argument. All arguments are to be specified along with data type and are separated by commas.

**Block of code:** It is a Set or Block of C statements, which will be executed during function call. Function definition execution will be performed in a stack.

If function has return type, then return statement will be the last statement of a block and if function has no return type, i.e., void then this function will have a no return statement.

*Let us Assume an example to solve the problem of function*

**Problem 1: Write a Function for addition of two numbers**

**Solution:**

+   1. First decide a meaningful name for the function like sum or addition, etc…
+   2. Now decide function Header statement, I am considering function name as sum, return_type as integer, and number of arguments and their respective data type.

```
    return_type sum(argument list)
```

sum function is going to add two integer variables, which means I need two integer variable as