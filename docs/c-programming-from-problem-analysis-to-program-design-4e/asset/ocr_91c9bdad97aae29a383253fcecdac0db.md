# EXAMPLE 5.11

```
```csharp
public static bool TryParse(string someStringValue, out int result)
```
```

When the TryParse() method is executed, result holds the integer value equivalent to the data stored in the string argument, someStringValue, or result stores a zero. If the string variable’s data is in the correct format and range, the conversion succeeds. Zero is only stored in someStringValue when the conversion fails. The conversion fails if the someStringValue parameter is null or has no value, is not of the correct format, or represents a number less than MinValue or greater than MaxValue of the integer.

> > **NOTE**
> >
> > Each of the built in data types have a TryParse() method. char.TryParse() converts the value of the specified string to its Unicode character equivalent; bool.TryParse() converts the specified string representation of a logical value to its Boolean equivalent. There are also TryParse() methods for decimal, double, and float. With each of these, in addition to doing the conversion, a Boolean value is returned indicating whether the conversion was successful or not.

As you review Example 5–11, notice that the parameter result has an out modifier listed before the data type. out parameters are output-only parameters meaning there is no value in result when the method is invoked. The parameter is considered initially unassigned. After the TryParse() method is executed, the out parameter result will hold either the converted value or zero.

When you input data, instead of just assuming the user will always enter valid characters, an if statement could be written to test the Boolean value returned from TryParse() as illustrated in Example 5–12.

# EXAMPLE 5.12

```
```csharp
if (int.TryParse(inValue, out v1) == false)
    Console.WriteLine("Did not put a valid integer - " +
                      "0 stored in v1");
```
```

> > **NOTE**
> >
> > Recall that when you use the special out and ref modifiers as part of the parameter, they must appear as part of the heading for the method and also in the call to the method.

The statement in Example 5–12 attempts to convert the string value stored in inValue into an integer, storing the result of the conversion in the variable v1. If it is successful, the