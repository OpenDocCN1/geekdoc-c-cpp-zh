
statement is that it provides multiple flows of control within a single iteration, which compromises readability. In Listing 4.53, the sample has been rewritten, replacing the continue statement with the if/else construct to demonstrate a more readable version that does not use the continue statement.

## LISTING 4.53: Replacing a continue Statement with an if Statement

```csharp
foreach (char letter in email)
{
    if (insideDomain)
    {
        System.Console.Write(letter);
    }
    else
    {
        if (letter == '@')
        {
            insideDomain = true;
        }
    }
}
```

## The goto Statement

Early programming languages lacked the relatively sophisticated “structured” control flows that modern languages such as C# have as a matter of course and instead relied on simple conditional branching (if) and unconditional branching (goto) statements for most of their control flow needs. The resultant programs were often hard to understand. The continued existence of a goto statement within C# seems like an anachronism to many experienced programmers. However, C# supports goto, and it is the only method for supporting fall-through within a switch statement. In Listing 4.54, if the /out option is set, code execution jumps to the default case using the goto statement, and similarly for /f.

## LISTING 4.54: Demonstrating a switch with goto Statements

```csharp
// ...
static void Main(string[] args)
{
    bool isOutputSet = false;
    bool isFiltered = false;
    foreach (string option in args)
    {
        switch (option)
        {
            case "/out":
                isOutputSet = true;
                isFiltered = false;
                goto default;
            case "/f":
                isFiltered = true;
                isRecursive = false;
                goto default;
            default:
                if (isRecursive)
                {
                    //Recurse down the hierarchy
                    //
                }
                else if (isFiltered)
                {
                    //Add option to list of filters
                    // ...
                }
                break;
        }
    }
    //...
}
```

Output 4.26 shows how to execute the code shown in Listing 4.54.

## OUTPUT 4.26

```text
C:\SAMPLES>Generate /out f1zbottle.bin /f"*.xml" "*.wsdl"
```

To branch to a switch section label other than the default label, you can use the syntax `goto case constant;`, where constant is the constant associated with the case label you wish to branch to. To branch to a statement that is not associated with a switch section, precede the target statement with any identifier followed by a colon; you can then use that identifier with the goto statement. For example, you could have a labeled statement `myLabel: Console.WriteLine();`. The statement `goto myLabel;` would then branch to the labeled statement. Fortunately, C# prevents you from using `goto` to branch into a code block; instead, `goto` may be used only to branch within a code block or to an enclosing code block. By making these restrictions, C# avoids most of the serious `goto` abuses possible in other languages.

In spite of the improvements, use of `goto` is generally considered to be inelegant, difficult to understand, and symptomatic of poorly structured code. If you need to execute a section of code multiple times or under different circumstances, either use a loop or extract code to a method of its own.

### Guidelines

- AVOID using `goto`.

## C# Preprocessor Directives

Control flow statements evaluate expressions at runtime. In contrast, the C# preprocessor is invoked during compilation. The preprocessor commands are directives to the C# compiler, specifying the sections of code to compile or identifying how to handle specific errors and warnings within the code. C# preprocessor commands can also provide directives to C# editors regarding the organization of code.

> **Language Contrast: C++—Preprocessing**
>
> Languages such as C and C++ use a **preprocessor** to perform actions on the code based on special tokens. Preprocessor directives generally tell the compiler how to compile the code in a file and do not participate in the compilation process itself. In contrast, the C# compiler handles “preprocessor” directives as part of the regular lexical analysis of the source code. As a result, C# does not support preprocessor macros beyond defining a constant. In fact, the term *preprocessor* is generally a misnomer for C#.

Each preprocessor directive begins with a hash symbol (#), and all preprocessor directives must appear on one line. A newline rather than a semicolon indicates the end of the directive.

A list of each preprocessor directive appears in Table 4.4.

## TABLE 4.4: Preprocessor Directives

| Statement or Expression | General Syntax Structure | Example |
| :--- | :--- | :--- |
| #if directive | `#if` preprocessor-expression | `#if` CSHARP2PLUS |
| | code | Console.Clear(); |
| | `#endif` | `#endif` |
| #elif directive | `#if` preprocessor-expression1 | `#if` LINUX |
| | code | ... |
| | `#elif` preprocessor-expression2 | `#elif` WINDOWS |
| | code | ... |
| | `#endif` | `#endif` |
| #else directive | `#if` | `#if` CSHARP1 |
| | code | ... |
| | `#else` | `#else` |
| | code | ... |
| | `#endif` | `#endif` |
| #define directive | `#define` conditional-symbol | `#define` CSHARP2PLUS |
| #undef directive | `#undef` conditional-symbol | `#undef` CSHARP2PLUS |
| #error directive | `#error` preproc-message | `#error` Buggy implementation |
| #warning directive | `#warning` preproc-message | `#warning` Needs code review |
| #pragma directive | `#pragma` warning | `#pragma` warning disable 1030 |
| #line directive | `#line` org-line new-line | `#line` 467 "TicTacToe.cs" ... |
| | `#line` default | `#line` default |
| #region directive | `#region` pre-proc-message | `#region` Methods |
| | code | ... |
| | `#endregion` | `#endregion` |

## Excluding and Including Code (#if, #elif, #else, #endif)

Perhaps the most common use of preprocessor directives is in controlling when and how code is included. For example, to write code that could be compiled by both C# 2.0 and later compilers and the prior version 1.0 compilers, you would use a preprocessor directive to exclude C# 2.0–specific code when compiling with a version 1.0 compiler. You can see this in the tic-tac-toe example and in Listing 4.55.

## LISTING 4.55: Excluding C# 2.0 Code from a C# 1.x Compiler

```csharp
#if CSHARP2PLUS
    System.Console.Clear();
#endif
```

In this case, you call the `System.Console.Clear()` method. Using the `#if` and `#endif` preprocessor directives, this line of code will be compiled only if the preprocessor symbol `CSHARP2PLUS` is defined.

Another use of the preprocessor directive would be to handle differences among platforms, such as surrounding Windows- and Linux-specific APIs with `WINDOWS` and `LINUX` `#if` directives. Developers often use these directives in place of multiline comments (`/* ... */`) because they are easier to remove by defining the appropriate symbol or via a search and replace.

A final common use of the directives is for debugging. If you surround code with an `#if DEBUG`, you will remove the code from a release build on most IDEs. The IDEs define the `DEBUG` symbol by default in a debug compile and `RELEASE` by default for release builds.

To handle an else-if condition, you can use the `#elif` directive within the `#if` directive instead of creating two entirely separate `#if` blocks, as shown in Listing 4.56.

## LISTING 4.56: Using #if, #elif, and #endif Directives

```csharp
#if LINUX
    ...
#elif WINDOWS
    ...
#endif
```

## Defining Preprocessor Symbols (#define, #undef)

You can define a preprocessor symbol in two ways. The first is with the `#define` directive, as shown in Listing 4.57.

## LISTING 4.57: A #define Example

```csharp
#define CSHARP2PLUS
```

The second method uses the `define` command line. Output 4.27 demonstrates this with Dotnet command-line interface.

## OUTPUT 4.27

```text
>dotnet.exe -define:CSHARP2PLUS TicTacToe.cs
```

Output 4.28 shows the same functionality using the csc.exe compiler directly.

## OUTPUT 4.28

```text
>csc.exe -define:CSHARP2PLUS TicTacToe.cs
```

To add multiple definitions, separate them with a semicolon. The advantage of the define compiler option is that no source code changes are required, so you may use the same source files to produce two different binaries.

To undefine a symbol, you use the #undef directive in the same way you use #define.

## Emitting Errors and Warnings (#error, #warning)

Sometimes you may want to flag a potential problem with your code. You do this by inserting #error and #warning directives to emit an error or a warning, respectively. Listing 4.58 uses the tic-tac-toe sample to warn that the code does not yet prevent players from entering the same move multiple times. The results of Listing 4.58 appear in Output 4.29.

## LISTING 4.58: Defining a Warning with #warning

```csharp
#warning "Same move allowed multiple times."
```

## OUTPUT 4.29

```text
Performing main compilation...
...\ticactoe.cs(471,16): warning CS1030: #warning: 'Same move allowed
multiple times.'
Build complete -- 0 errors, 1 warnings
```

By including the #warning directive, you ensure that the compiler will report a warning, as shown in Output 4.29. This particular warning is a way
