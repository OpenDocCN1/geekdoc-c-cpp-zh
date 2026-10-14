+   - Eric Lippert explains *why* initializers for read-only fields and constructors run in the order they do at https://docs.microsoft.com/en-gb/archive/blogs/ericlippert/why-do-initializers-run-in-the-opposite-order-as-constructors-part-one.
+   - Lippert has written extensively on the subject of value types in C#, including the following:
+     - “The Truth About Value Types,” https://docs.microsoft.com/en-gb/archive/blogs/ericlippert/the-truth-about-value-types
+     - “The Stack Is an Implementation Detail, Part One,” https://docs.microsoft.com/en-gb/archive/blogs/ericlippert/the-stack-is-an-implementation-detail-part-one
+     - “The Stack Is an Implementation Detail, Part Two,” https://docs.microsoft.com/en-gb/archive/blogs/ericlippert/the-stack-is-an-implementation-detail-part-two
+   - Nullable reference types are documented by Microsoft at https://docs.microsoft.com/en-us/dotnet/csharp/nullable-references.
+   - Additionally, Jon Skeet blogs about his early experiences with nullable reference types at https://codeblog.jonskeet.uk/2018/04/21/first-steps-with-nullable-reference-types/.
+   - Tony Hoare made his famous apology for the null reference at the QCon conference in 2009. The abstract is available at https://qconlondon.com/london-2009/qconlondon.com/london-2009/presentation/Null%2bReferences_%2bThe%2bBillion%2bDollar%2bMistake.html.

# Chapter 3

+   - The C# Language Specification describes the variable categories at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/variables.
+   - The rules regarding definite assignment are also described in the C# Language Reference at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/variables#94-definite-assignment.
+   - Jon Skeet looks at parameter passing by reference and by value in his blog at https://jonskeet.uk/csharp/parameters.html.
+   - The third edition of C# in Depth by Jon Skeet (Manning, 2014) has a detailed analysis of closures in Chapters 5 and 16.
+   - Closures are not new to C#, but their behavior has changed in some ways; capturing a loop variable is one example. Eric Lippert’s blog has a good article on the rationale behind the old (pre-C# v5) behavior of capturing loop variables in function objects: https://ericlippert.com/2009/11/12/closing-over-the-loop-variable-considered-harmful-part-one/.
+   - An overview of several C# features for efficient code, including read-only structs and in parameters, is at https://docs.microsoft.com/en-us/dotnet/csharp/write-safe-efficient-code.