# New Line

When writing out a new line, the exact characters for the new line will depend on the operating system on which you are executing. On Microsoft Windows platforms, the new line is the combination of both the ‘\r’ and ‘\n’ chars, while a single ‘\n’ is used on Unix. One way to overcome the discrepancy between platforms is simply to use System.Console.WriteLine() in order to output a blank line. Another approach, virtually essential when you are not outputting to the console yet still require execution on multiple platforms, is to use System.Environment.NewLine. In other words, System.Console.WriteLine("Hello World") and System.Console.Write("Hello World" + System.Environment.NewLine) are equivalent.

# ADVANCED TOPIC

# C# Properties

Technically, the Length member referred to in the following section is not actually a method, as indicated by the fact that there are no parentheses following its call. Length is a property of string, and C# syntax allows access to a property as though it were a member variable (known in C# as a field). In other words, a property has the behavior of special methods called setters and getters, but the syntax for accessing that behavior is that of a field.

Examining the underlying CIL implementation of a property reveals that it compiles into two methods: set_<PropertyName> and get_<PropertyName>. Neither of these, however, is directly accessible from C# code, except through the C# property constructs. See Chapter 5 for more detail on properties.

# String Length

To determine the length of a string you use a string member called Length. This particular member is called a read-only property. As such, it can’t be set, nor does calling it require any parameters. Listing 2.13 demonstrates how to use the Length property, and Output 2.11 shows the results.