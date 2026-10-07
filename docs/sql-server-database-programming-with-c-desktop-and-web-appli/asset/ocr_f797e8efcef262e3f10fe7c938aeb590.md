# 166                               SQL Server Database Programming with C#

```
public static class Conversion
{
    public static string ConvertToUpper(string input)
    {
        return input.ToUpper();
    }
    public static string ConvertToLower(string input)
    {
        return input.ToLower();
    }
}
```

**FIGURE 4.61** Example of instance method ConvertToUpper.

```
// call instance method ConvertToUpper.
// first create a new instance of the class Conversion
Conversion conv = new Conversion("conversion");
string instResult = conv.ConvertToUpper("conversion");
// call method ConvertToLower.
string classResult = Conversion.ConvertToLower("CONVERSION");
```

**FIGURE 4.62** An example of calling class and instance method.

with the class name prefixed in that of method. Figure 4.62 shows a piece of code to call of these two methods.
In some situations, the query would become very complicated if one wants to call static methods from any instance of those classes. To solve this complex issue, extension methods are developed to simplify the query structures and syntax.
To declare an extension method from existing static method, just add the keyword to the first argument of static method. For example, to make the method ConvertToLower() an extension method, add the keyword to the first argument of that method, as shown in Figure 4.63.
Now the class method ConvertToLower() has been converted to an extension method and can be accessed by any instance of the class Conversion.
The extension methods have the following important properties:

+   1. The extension method will work as an instance method of any object with the same type as the extension method's first argument data type.
2. The extension methods can only be declared in static classes.
3. Both the class and the extension method are prefixed by the keyword static.

```
public static class Conversion
{
    // declare the class method ConvertToLower to extension method.
    public static string ConvertToLower(this string input)
    {
        return input.ToLower();
    }
}
```

**FIGURE 4.63** Declare the class method ConvertToLower() to extension method.