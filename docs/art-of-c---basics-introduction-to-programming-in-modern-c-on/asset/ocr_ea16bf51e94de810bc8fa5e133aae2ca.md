![](bbox=[0.11, 0.08, 0.17, 0.13])

The line numbers, printed on the left-hand side, are not part of the program. They are included for easy reference in this book.

# 2.2.1. Explanation

This example program includes a few more lines of code. You can run the program as before:

```
dotnet run
```

It produces the following output:

```
Hello Joe!!!
```

# 2.2.2. Grammar

As in the earlier examples, this source code file, the only file in the program, includes the “top-level statements” (and, nothing else). When you build and run the program, the top-level statements will be executed, more or less from top to bottom.

This program also includes the `Console.WriteLine()` statement, and we rely on the implicit namespace inclusion. That is, the `using System` declaration is implied, as specified in the project XML file.

The first line of the program defines a “string constant” named `name`.

```
const string name = "Joe";
```

Note the syntax. This statement starts with the `C#` keyword `const`, followed by a type name, `string` in this case, and the name of the constant, `name` in this case. The left-hand side of this statement declares a new constant `name` with a type `string`. It