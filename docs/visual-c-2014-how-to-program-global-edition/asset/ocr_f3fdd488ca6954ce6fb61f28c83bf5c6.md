# 7.13 Optional Parameters

# 7.12.3 Return Types of Overloaded Methods

In discussing the logical names of methods used by the compiler, we did not mention the methods' return types. Methods cannot be distinguished by return type. If in a class MethodOverloadError you define methods with the following headers:

```
int Square(int x)
double Square(int x)
```

which has the same signature but different return types, the compiler generates the following error for the second Square method:

Type 'MethodOverloadError' already defines a member called 'Square' with the same parameter types

Overloaded methods can have the same or different return types if the parameter lists are different. Also, overloaded methods need not have the same number of parameters.

# Common Programming Error 7.9

> Declaring overloaded methods with identical parameter lists is a compilation error regardless of whether the types are different.

![](bbox=[0.143, 0.366, 0.213, 0.403])

# 7.13 Optional Parameters

Methods can allow the calling method to vary the number of arguments to pass. An optional parameter specifies a default value that is assigned to the parameter if the optional argument is omitted. You can create methods with one or more optional parameters. All optional parameters must be placed to the right of the method's optional parameters—that is, at the end of the parameter list.

# Common Programming Error 7.10

> Declaring a non-optional parameter to the right of an optional one is a compilation error.

![](bbox=[0.143, 0.574, 0.213, 0.611])

When a method has a default value, the caller has the option of passing that particular argument. For example, the method header

```
static int Power(int baseValue, int exponent = 2)
```

specifies an optional argument. Each call to Power must pass at least a baseValue, or a compilation error occurs. Optionally, the exponentValue parameter can be passed to Power. Each optional parameter must specify a default value by using an equal (=) sign followed by value. For example, the method header sets Power 2 as exponentValue's default value. Consider the following calls to Power:

+   * Power()—This calls a compilation error because this method requires a minimum of one argument.
* Power(10)—This is valid because one argument (10) is being passed. The exponentValue is not specified in the call, so the compiler uses 2 for the exponentValue, as specified in the method header.
* Power(10, 3)—This call is also valid because 10 is passed as the required argument and 3 is passed as the optional argument.