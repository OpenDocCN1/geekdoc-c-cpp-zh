Placing void prior to Main() indicates that this method does not return any data (explained further in Chapter 2).

One distinctive C/C++ style characteristic followed by C# is the use of curly braces for the body of a construct, such as the class or the method. For example, the Main method contains curly braces that surround its implementation; in this case, only one statement appears in the method.

# Statements and Statement Delimiters

The Main method includes a single statement, System.Console.WriteLine(), which is used to write a line of text to the console. C# generally uses a semicolon to indicate the end of a statement, where a statement comprises one or more actions that the code will perform. Declaring a variable, controlling the program flow, and calling a method are examples of statements.

Language Contrast: Visual Basic—Line-Based Statements
Some languages are line-based, meaning that without a special annotation, statements cannot span a line. Until Visual Basic 2010, Visual Basic was an example of a line-based language. It required an underscore at the end of a line to indicate that a statement spans multiple lines. Starting with Visual Basic 2010, many cases were introduced where the line continuation character was optional.

# ADVANCED TOPIC

# Statements without Semicolons

Many programming elements in C# end with a semicolon. One example that does not include the semicolon is a switch statement. Because curly braces are always included in a switch statement, C# does not require a semicolon following the statement. In fact, code blocks themselves are considered statements (they are also composed of statements) and they don't require closure using a semicolon. Similarly, there are cases, such as the using declarative, in which a semicolon occurs at the end but it is not a statement.