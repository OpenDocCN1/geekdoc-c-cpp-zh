# [Execution Result]

Hello from traditional namespace!
Hello from file-scoped namespace!

In traditional C# code, the namespace keyword wraps all the content inside a block, requiring extra indentation and braces {}.

With the introduction of file-scoped namespaces in C# 10, you can now end the namespace declaration with a semicolon ;

which tells the compiler that all subsequent types (classes, interfaces, etc.) belong to this namespace—without needing a block.

This makes files easier to read and avoids deep nesting, especially in large projects.

# Important Notes:

This feature requires C# 10 or later, so make sure your project is targeting .NET 6 or later.

You can only have one file-scoped namespace per file.

This change is purely syntactic—there's no behavioral difference at runtime.

This feature is especially useful for developers transitioning from other languages that use flat or simplified module structures.

# [Supplement]

The syntax namespace Name; was inspired by modern languages that favor simplicity, like Python (which uses modules) and JavaScript (which