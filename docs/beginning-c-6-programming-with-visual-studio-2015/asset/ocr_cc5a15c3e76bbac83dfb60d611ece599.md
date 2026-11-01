If checkVal is >= 5, then no return statement is met, which isn't allowed. All processing paths must reach a return statement. In most cases, the compiler detects this and gives you the error "not all code paths return a value."

Functions that execute a single line of code can use a feature introduced in C# 6 called expression-bodied methods. The following function pattern uses a => (lambda arrow) to implement this feature.

```
static <returnType> <FunctionName>() => <myVal1> * <myVal2>;
```

For example, a Multiply() function which prior to C# 6 is written like this:

```
static double Multiply(double myVal1, double myVal2)
{
    return myVal1 * myVal2;
}
```

Can now be written using the => (lambda arrow). The result of the code written here expresses the intent of the method in a much simpler and consolidated way.

```
static double Multiply(double myVal1, double myVal2) => myVal1 * MyVal2;
```

# Parameters

When a function needs to accept parameters, you must specify the following:

+   - A list of the parameters accepted by the function in its definition, along with the types of those parameters
+   - A matching list of arguments in each function call

> NOTE Note that careful reading of the C# specification shows a subtle distinction between parameters and arguments. Parameters are defined as part of a function definition, whereas arguments are passed to a function by calling code. However, these terms are often used interchangeably, and nobody seems to get too upset about that.

This involves the following code, where you can have any number of parameters, each with a type and a name:

```
static <returnType> <FunctionName>(<paramType> <paramName>, ...)
{
    ...
    return <returnValue>;
}
```

The parameters are separated using commas, and each of these parameters is accessible from code within the function as a variable. For example, a simple function might take two double parameters and return their product:

```
static double Product(double param1, double param2) => param1 * param2;
```