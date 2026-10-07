
# C# Preprocessor Directives

directives to the C# compiler, specifying the sections of code to compile or identifying how to handle specific errors and warnings within the code. C# preprocessor commands can also provide directives to C# editors regarding the organization of code.

# Language Contrast: C++

Languages as C and C++ use a preprocessor to perform actions on the code based on special tokens. Preprocessor directives generally tell the compiler how to compile the code in a file and do not participate in the compilation process itself. The C compiler handles "preprocessor" directives as of the regular lexical analysis of the source code. As a result, C does not support preprocessor macros beyond defining a constant. In fact, the term preprocessor is generally a misnomer in C.

Each preprocessor directive begins with a hash symbol (#), and all preprocessor directives must appear on one line. A newline rather than a semicolon indicates the end of the directive.

A list of each preprocessor directive appears in Table 4.5.

# TABLE 4.5: Preprocessor Directives

| Statement or Expression | General Syntax Structure | Example |
|---|---|--|
| #if directive | #if preprocessor-expression<br>code<br>#endif | #if CSHARPPLUS<br>Console.Clear();<br>#endif |
| #elif directive | #if preprocessor-expression1<br>code<br>#elif preprocessor-expression2<br>code<br>#endif | #if LINUX<br>#elif WINDOWS<br>. .<br>#endif |
| #else directive | #if<br>#else<br>code<br>#endif | #if CSHARP1<br>. ..<br>#else<br>code<br>#endif |
| #define directive | #define conditional-symbol | #define CSHARPPLUS |
| #undef directive | #undef conditional-symbol | #undef CSHARPPLUS |

# Chapter 4: Operators and Control Flow

Table 4.5: Preprocessor Directives (continued)

| Statement or Expression | General Syntax Structure | Example |
|--- | --- |--- |
| #error directive | #error preproc-message | #error Debug implementation |
| #warning directive | #warning preproc-message | #warning Needs code review |
| #pragma directive | #pragma warning | #pragma warning disable 1030 |
| #line directive | #line org-line new-line | #line 467 "*TicTacoe.cs" #line default |
| | #line default | |
| #region directive | #region pre-proc-message code #endregion | #region Methods ... #endregion |
| #nullable directive | #nullable enable | disable | restore | #nullable enable ..string? text = null; #nullable restore |

# Excluding and Including Code (#if, #elif, #else, #endif)

Perhaps the most common use of preprocessor directives is in controlling and and how code is included. For example, to write code that could be compiled by both C# 2.0 and later compilers and the prior version 1.0 compilers, you would use a preprocessor directive to exclude C# 2.0-specific code when compiling with a version 1.0 compiler. You can see this in the tic-tac-toe example and in Listing 4.56.

Listing 4.56: Excluding C# 2.0 Code from a C# 1.x Compiler

```
#if CSHARP2PLUS
System.Console.Clear();
#endif
```

In this case, you call the System.Console.Clear() method. Using the #if and #endif preprocessor directives, this line of code is compiled only if the preprocessor symbol CSHARP2PLUS is defined.

# C# Preprocessor Directives 209

Another use of preprocessor directives would be to handle differences among platforms, such as surrounding Windows- and Linux-specific APIs with WINDOWS and LINUX #if directives. Developers use these directives in place of multiline comments (/**/) because they are easier to remove by defining the appropriate symbol or via a search and replace.

A final use of the directives is for debugging. If you surround your code with an # DEBUG, you will remove the code from a release build on most IDEs. The IDEs define the DEBUG symbol by default in a debug compile and RELEASE by default for release builds.

To handle an else-if condition, you can use the #elif directive within the #if directive instead of creating entirely separate #if blocks, as shown in Listing 4.57.

LISTING 4.57: Using #if, #elif, and #endif Directives

```
#if LINUX
//...
#elif WINDOWS
//...
#endif
```

# Defining Preprocessor Symbols (#define, #undef)

You can define a preprocessor symbol in two ways. The first is with the #define directive, as shown in Listing 4.58.

LISTING 4.58: A #define Example

```
#define CSHARP2PLUS
```

The second method uses the define command line. Output 4.27 demonstrates this with Dotnet command-line interface.

OUTPUT 4.27

```
>dotnet.exe -define:CSHARP2PLUS TicTac.cs
```

To add multiple definitions, separate them with a semicolon. The advantage of the define compiler option is that no source code changes are required, so you may use the same source files to produce two different binaries.

To undefine a symbol, you use the #undef directive in the same way you use #define.

# Emitting Errors and Warnings (#error, #warning)

Sometimes you may want to flag a potential problem with your code. You do this by inserting #error and #warning directives to emit an error or a warning, respectively. Listing 4.59 uses the tic-tac-toe example to warn that the code does not prevent players from entering the same multiple times. The results of Listing 4.59 appear in Output 4.28.

LISTING 4.59: Defining a Warning with #warning

```
#warning "Same move allowed multiple times."
```

OUTPUT 4.28

```
Performing main compilation...
...tictactoe.cs(471,16): warning CS1030: #warning: ''Same move allowed multiple times.''
Build complete -- 0 errors, 1 warnings
```

By including the #warning directive, you ensure the compiler will report a warning, as shown in Output 4.28. This particular warning is a way of flagging the fact that there is a potential enhancement or bug within the code. It could be a simple way of reminding the developer of a pending task.

# C# Preprocessor Directives

# Turning Off Warning Messages (#pragma)

Warnings are helpful because they point to code that could potentially be troublesome. However, sometimes it is preferred to turn off specific warnings explicitly because they can be ignored legitimately. C# provides the preprocessor #pragma directive for this purpose (see Listing 4.60).

-   LISTING 4.60: Using the Preprocessor #pragma Directive to Disable the #warning Directive

```
#pragma warning disable CS1030
```

To reenable the warning, #pragma supports the restore option following the warning, as shown in Listing 4.61.

-   LISTING 4.61: Using the Preprocessor #pragma Directive to Restore a Warning

```
#pragma warning restore CS1030
```

In combination, these two directives can surround a particular block of code where the warning is explicitly determined to be irrelevant.

Perhaps one of the most common warnings to disable is CS1591. This warning appears when you elect to generate XML documentation using the /doc compiler option, but you neglect to document all of the public items within your program.

Code warnings occur frequently throughout this book because listings often are incomplete—that is, we are showing initial code snippets that aren't fully developed. To suppress the warnings, which are not relevant in an example scenario, we add #pragma directives to the file. Table 4.6 provides an example of some of the warnings that are disabled within Chapter 4.

-   TABLE 4.6: Sample Warnings

| Category | Warning |
|---|---|
| CS0168 | Variable is declared but never used |

6. Introduced in C# 2.0.

# Chapter 4: Operators and Control Flow

| Category | Warning |
|---|---|
| CS0219 | Variable is assigned but its value is never used |
| IDE0059 | Unnecessary assignment of a value |

Note that C# warning numbers are prefixed with the letters CS in the compiler output, a prefix that is optional in the #pragma directive. however, there are other prefixes like “IDE” that are part of the identity. The IDE059 message is an example.

# nowarn:<list> Option

In addition to the #pragma directive, C# compilers generally support the nowarn=<list> option. This achieves the same result as #pragma, except instead of adding it to the source code, you can insert the command as a compiler option. The nowarn option affects the entire compilation, whereas #pragma affects only the file in which it appears. To turn off the CS0219 warning, for example, you would use the command as shown in Output 4.29.

# OUTPUT 4.29

```
> dotnet build /p:NoWarn="0219"
```

# Specifying Line Numbers (#line)

The #line directive controls on which line number the C# compiler reports an error or warning. It is used predominantly by utilities and designers that emit C# code. In Listing 4.62, the actual line numbers within the file appear on the left.
