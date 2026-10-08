# 7.15 C# 6 Expression-Bodied Methods and Properties 313

+   - t.SetTime()—This call specifies no arguments, so the compiler assigns the default value 0 to each parameter. The resulting time is 2:00:00 AM.
- t.SetTime(12)—This call specifies the argument 12 for the first parameter, hour, and the compiler assigns the default value 0 to the minute and second parameter. The resulting time is 12:00:00 PM.
- t.SetTime(12, 30)—This call specifies the arguments 12 and 30 for the parameters hour and minute, respectively, and the compiler assigns the default value 0 to the parameter second. The resulting time is 12:30:00 PM.
- t.SetTime(12, 30, 22)—This call specifies the arguments 12, minute, and 22, respectively, so the compiler does not provide any default values. The resulting time is 12:30:22 PM.

If you wanted to specify only the hour and second? You might think that you could call the method as:
`t.SetTime(12, 22); // COMPILATION ERROR`
# doesn't allow you to skip an argument as shown above. C# provides a feature called named parameters, which enables you to call methods that receive optional parameters by providing only the arguments you want to specify. So, you explicitly specify the parameter's name and value—separated by a colon)—in the argument list of the method. For example, the preceding statement can be written as:
`t.SetTime(hour: 12, second: 22); // sets the time to 12:00:22`

In this case, the compiler assigns hour the argument 12 and second the argument 22. The parameter minute is not specified, so the compiler assigns the default value 0. It is also possible to specify the arguments out of order when using named parameters. The arguments for the required parameters must always be supplied. The argumentName syntax may be used with any method's parameters.

# 7.15 C# 6 Expression-Bodied Methods and Properties 6

C# 6 introduces a concise syntax for:

+   - methods that contain only a return statement that returns a value
- read-only properties in which the getter contains only a return statement
- methods that contain single statement statement body.

Consider the following method:

```
static int Cube(int x)
{
    return x * x * x;
}
```

In C# 6, this can be expressed with an expression-bodied method as
`static int Cube(int x) => x * x * x;`
The value of x * x * x is returned to Cube's caller implicitly. The symbol follows the method's parameter list and introduces the method's body—no braces or return statement are required and can be used with static and non-static methods alike. If the