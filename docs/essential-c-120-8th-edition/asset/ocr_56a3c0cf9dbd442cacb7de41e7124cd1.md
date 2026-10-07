# 68 Chapter 2: Data Types

LISTING 2.14: Displaying a Triangle Using a Verbatim String Literal

```
Console.Write(@"Begin
  /\
 / \\
  /\\
End"");
```

OUTPUT 2.10

![](bbox=[0.132, 0.288, 0.842, 0.412])

Without the @ character, this code would not even compile. In fact, even if you
changed the shape to a square, eliminating the backslashes, the code still would not
compile because a newline cannot be placed directly within a string literal that is not
prefaced with the \u00e symbol.

The only escape sequence the verbatim string does support is "", which
signifies a single set of double quotes and does not terminate the string.

# Language Contrast: C++—String Concatenation at
Compile Time

Unlike C++, C# does not automatically concatenate literal strings. You cannot, for
example, specify a string literal as follows:

> "Major Strasser has been shot."
"Round up the usual suspects."

Rather, concatenation requires the use of the addition operator (+). If the
compiler can calculate the result at compile time, however, the resultant CIL code
will be a single string.

If the same literal string appears within an assembly multiple times, the compiler
will define the string only once within the assembly and all variables will refer to the