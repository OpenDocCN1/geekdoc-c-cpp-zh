View Demo

Or they can be formatted as dates:

```
Console.WriteLine($"Today is: {eTime.Today:dddd, MMMM dd - yyyy}");
```

Output:

Today is: Monday, July, 20 - 2015

View Demo

Statements with a Conditional (Ternary) Operator can also be evaluated within the interpolation. However, these must be wrapped in parentheses, since the colon is otherwise used to indicate formatting as shown above:

```
Console.WriteLine($"{{foo > bar ? \"Foo is larger than bar!\" : \"Bar is larger than foo!\"}}");
```

Output:

Bar is larger than foo!

View Demo

Conditional expressions and format specifiers can be mixed:

```
Console.WriteLine($"Environment: {(Environment.Is64BitProcess ? 64 : 32):00'-bit'} process");
```

Output:

Environment: 32-bit process

# Escape sequences

Escaping backslash (\ ) and quote (") characters works exactly the same in interpolated strings as in non-interpolated strings, for both verbatim and non-verbatim string literals:

```
Console.WriteLine($"Foo is: {foo}. In a non-verbatim string, we need to escape \" and \\ with backslashes.");
```

```
Console.WriteLine($"@Foo is: {{foo}}. In a verbatim string, we need to escape \"\" with an extra quote, but we don't need to escape \");
```

Output:

Foo is 34. In a non-verbatim string, we need to escape " and \ with backslashes.
Foo is 34. In a verbatim string, we need to escape " with an extra quote, but we don't need to escape \

To include a curly brace { or } in an interpolated string, use two curly braces {{ or }}:$"{{foo}} is: }"

Output:

{foo} is: 34