```
EXAMPLE 3.4
```csharp
Console.Write(int)
Console.Write(double)
Console.Write(object)
Console.Write(bool)
```
```

So how does the CLR know which of these 18 methods to use? The answer is simple, but important for you to understand. When the method is called, the argument used to make the call is matched with the signature to determine which of the methods to execute. Remember, the signature of the method includes the formal parameters, which include the data type that can be used for the method.

In Visual Studio, after you select the `Write()` member and type the opening parenthesis, IntelliSense displays a drop-down list with a scroll bar that allows the viewing of all 18 signatures. This gives you an opportunity to know what type of argument is needed with a call. Figure 3-3 shows the first of the 18 signatures.

![](bbox=[0.1859, 0.414, 0.9119, 0.533])

**FIGURE 3-3** IntelliSense display

The `Write()` method in Figure 3-3 is called by entering the name of the method, an open parenthesis, a `string` value, and a closing parenthesis. In the call, the `string` value can be a string literal, a string variable, or a value of another data type converted to a string. From Chapter 2, you learned that a string literal is one or more characters enclosed in double quotation marks. A valid call to the `Write()` method using the displayed overloaded method from Figure 3-3 would be:

```
Console.Write("Any string value will work!");
```

The 18 overloaded `Write()` methods include parameters for common types, such as `int`, `double`, `decimal`, `bool`, and `object`. You should explore the other options.

# WriteLine() Method

As shown previously, the `WriteLine()` method behaves like the `Write()` method with the exception that it writes the current end-of-line terminator after it displays the