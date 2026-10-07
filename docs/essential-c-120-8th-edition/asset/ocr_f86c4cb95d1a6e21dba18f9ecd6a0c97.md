# C# Syntax Fundamentals ▄ ▄ 13

where statement comprises one or more actions that the code will perform.
Declaring a variable, controlling the program flow, and calling a method are typical
uses of statements.

# ADVANCED TOPIC

Statements without Semicolons
Many programming elements in C# end with a semicolon. One example that does
not include the semicolon is a switch statement. Because curly braces are always
included in a switch statement, C# does not require a semicolon following the
statement. In fact, code blocks themselves are considered statements (they are also
composed of statements), and they don't require ending with a semicolon. Similarly,
there are cases, such as using the declaration, in which a semicolon appears as
postfix, but it is not a statement.

Since creation of a newline does not separate statements, you can place multiple
statements on the same line, and the C# compiler will interpret the line as having
multiple instructions. For example, Listing 1.3 contains two statements on a single
line that, in combination, display Up and Down on two separate lines.

# LISTING 1.3: Multiple Statements on One Line

```
Console.WriteLine("Up"); Console.WriteLine("Down");
```

Similarly, each statement can be placed on its own line, as shown in Listing 1.4.

# LISTING 1.4: Multiple Statements Each on Separate Lines

```
Console.WriteLine("Down");
Console.WriteLine("Side");
Console.WriteLine("Up");
```

C# also allows the splitting of a statement across multiple lines. Again, the C#
compiler looks for a semicolon to indicate the end of a statement. In Listing 1.5, for
example, the original WriteLine() statement from the HelloWorld program is
split across multiple lines.