# 2.2. Top-Level Statements

Since C# 9, one source file in a program may use top-level statements as long as the program does not include any other entry point methods. It is a syntactic sugar to help remove some boilerplate code. The top-level statements are automatically wrapped in the Main method of an implicitly defined startup class.

Top-level statements can access the command line arguments using the implicitly defined variable args of type

If the top-level statements return an integer value, that value becomes the integer return code to the operating system/runtime.

The top-level statements may contain async expressions.

For example,

```
Console.WriteLine("Hello World");
```

A file including this one line of code, using the implicit global using feature available since C# 10, is more or less equivalent to something like the following:

```
namespace Namespacel {
    class Program {
```