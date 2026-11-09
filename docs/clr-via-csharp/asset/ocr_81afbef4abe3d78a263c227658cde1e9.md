C# offers some special syntax to help you enter literal strings into the source code. For special characters such as new lines, carriage returns, and backspaces, C# uses the escape mechanism familiar to C/C++ developers.

```
```csharp
// String containing carriage-return and newline characters
String s = "Hi\r\nhere.";
```
```

![](bbox=[0.088, 0.207, 0.137, 0.246])

> > **Important** Although the preceding example hard-codes carriage-return and newline characters into the string, I don't recommend this practice. Instead, the `System.Environment` type defines a read-only **NewLine** property that returns a string consisting of these characters when your application is running on Microsoft Windows. However, the **NewLine** property is platform sensitive, and it returns the appropriate string required to obtain a newline by the underlying platform. So, for example, if the Common Language Infrastructure (CLI) is ported to a UNIX system, the **NewLine** property would return a string consisting of just a single character \n. Here's the proper way to define the previous string so that it works correctly on any platform:
> >
> > ```csharp
> > String s = "Hi" + Environment.NewLine + "there.";
> > ```

You can concatenate several strings to form a single string by using C#'s + operator as follows:

```
```csharp
// Three literal strings concatenated to form a single literal string
String s = "Hi" + " " + "there.";
```
```

In this code, because all of the strings are literal strings, the C# compiler concatenates them at compile time and ends up placing just one string—"Hi there."—in the module's metadata. Using the + operator on nonliteral strings causes the concatenation to be performed at runtime. To concatenate several strings together at runtime, avoid using the + operator because it creates multiple string objects on the garbage-collected heap. Instead, use the `System.Text.StringBuilder` type (which I'll explain later in this chapter).

Finally, C# also offers a special way to declare a string in which all characters between quotes are considered part of the string. These special declarations are called verbatim strings and are typically used when specifying the path of a file or directory or when working with regular expressions. Here is some code showing how to declare the same string with and without using the verbatim string character (@).

```
```csharp
// Specifying the pathname of an application
String file = "C:\\Windows\\System32\\Notepad.exe";

// Specifying the pathname of an application by using a verbatim string
String file = @"C:\Windows\System32\Notepad.exe";
```
```