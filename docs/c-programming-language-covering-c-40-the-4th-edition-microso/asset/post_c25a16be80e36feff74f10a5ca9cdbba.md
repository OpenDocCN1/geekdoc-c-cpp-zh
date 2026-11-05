
As indicated by the syntax, conditional compilation directives must be written as sets consisting of, in order, an #if directive, zero or more #elif directives, zero or one #else directive, and an #endif directive. Between the directives are conditional sections of source code. Each section is controlled by the immediately preceding directive. A conditional section may itself contain nested conditional compilation directives provided these directives form complete sets.

> CHRIS SELLS  I can see #if and #endif, but #elif? Is this a Santa’s helper with a lisp? A hipster abbreviation for some large, gray, wrinkled animal? I’d have preferred springing for the two extra characters in #elseif simply so I could actually remember it...

A pp-conditional selects at most one of the contained conditional-sections for normal lexical processing;

- The pp-expressions of the #if and #elif directives are evaluated in order until one yields true. If an expression yields true, the conditional-section of the corresponding directive is selected.
- If all pp-expressions yield false, and if an #else directive is present, the conditional-section of the #else directive is selected.
- Otherwise, no conditional-section is selected.

The selected conditional-section, if any, is processed as a normal input-section: The source code contained in the section must adhere to the lexical grammar; tokens are generated from the source code in the section; and preprocessing directives in the section have the prescribed effects.

The remaining conditional-sections, if any, are processed as skipped-sections: Except for preprocessing directives, the source code in the section need not adhere to the lexical grammar; no tokens are generated from the source code in the section; and preprocessing directives in the section must be lexically correct but are not otherwise processed. Within a conditional-section that is being processed as a skipped-section, any nested conditional-sections (contained in nested #if...#endif and #region...#endregion constructs) are also processed as skipped-sections.

The following example illustrates how conditional compilation directives can nest:

```
#define Debug      // Debugging on
#undef Trace      // Tracing off
class PurchaseTransaction
{
void Commit() {
    #if Debug
    CheckConsistency();
    #if Trace
    WriteToLog(this.ToString());
    #endif
    #endif
    CommitHelper();
}
}
```

Except for preprocessing directives, skipped source code is not subject to lexical analysis. For example, the following is valid despite the unterminated comment in the #else section:

```
#define Debug      // Debugging on
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #else
        // Do something else
        #endif
    }
}
```

Note, however, that preprocessing directives are required to be lexically correct even in skipped sections of source code.

> CHRIS SELLS  Avoid the use of nested preprocessing directives if you can, simply because by default the most popular C# editor on the planet, Visual Studio, will arrange them along the left edge of your text file, making it very difficult to follow the nesting. For example,

```
#define Debug      // Debugging on
#undef Trace       // Tracing off
class PurchaseTransaction {
void Commit() {
#if Debug
    CheckConsistency();
#if Trace
    WriteToLog(this.ToString());
#endif
#endif
    CommitHelper();
}
}
```

Preprocessing directives are not processed when they appear inside multi-line input elements. For example, the program

```
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello,
#if Debug
        World
#else
        Nebraska
#endif
        ");
    }
}
```

results in the output:

```
hello,
#if Debug
        World
#else
        Nebraska
#endif
```

In peculiar cases, the set of preprocessing directives that is processed might depend on the evaluation of the pp-expression. The example

```
#if X
    /*
#else
    /* */ class Q { }
#endif
```

always produces the same token stream (class Q { }), regardless of whether X is defined. If X is defined, the only processed directives are #if and #endif, due to the multi-line comment. If X is undefined, then three directives (#if, #else, #endif) are part of the directive set.

## 2.5.5 Diagnostic Directives

The diagnostic directives are used to explicitly generate error and warning messages that are reported in the same way as other compile-time errors and warnings.

```
pp-diagnostic:
    whitespace     # whitespace   error   pp-message
    whitespace_opt # whitespace   warning pp-message
```

```
pp-message:
    new-line
    whitespace input-characters_opt new-line
```

### The example

```
#warning Code review needed before check-in
#if Debug && Retail
    #error A build can't be both debug and retail
#endif
class Test {...}
```

always produces a warning ("Code review needed before check-in"), and produces a compile-time error ("A build can't be both debug and retail") if the conditional symbols Debug and Retail are both defined. Note that a pp-message can contain arbitrary text; specifically, it need not contain well-formed tokens, as shown by the single quote in the word can't.

## 2.5.6 Region Directives

The region directives are used to explicitly mark regions of source code.

```
pp-region:
    pp-start-region conditional-section_opt pp-end-region
```

```
pp-start-region:
    whitespace_opt # whitespace_opt region pp-message
```

```
pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

No semantic meaning is attached to a region; regions are intended for use by the programmer or by automated tools to mark a section of source code. The message specified in a #region or #endregion directive likewise has no semantic meaning; it merely serves to identify the region. Matching #region and #endregion directives may have different pp-messages.

The lexical processing of a region

```
#region
...
#endregion
```

corresponds exactly to the lexical processing of a conditional compilation directive of the form:

```
#if true
...
#endif
```

## 2.5.7 Line Directives

Line directives may be used to alter the line numbers and source file names that are reported by the compiler in output such as warnings and errors.

Line directives are most commonly used in meta-programming tools that generate C# source code from some other text input.

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
```

```
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
```

```
file-name:
    " file-name-characters "
```

```
file-name-characters:
    file-name-characters file-name-character
```

```
file-name-character:
    Any input-character except "
```

When no #line directives are present, the compiler reports true line numbers and source file names in its output. When processing a #line directive that includes a line-indicator that is not default, the compiler treats the line after the directive as having the given line number (and file name, if specified).

> **JON SKEET** If you’re writing a tool that generates code from some other source, you might think that the easiest approach is to just include a #line directive for every line you output. It’s not quite that simple, however: A #line directive within a verbatim string literal ends up as part of the string, rather than being treated as a directive. So the following code almost certainly doesn’t work as intended:

```
#line 5
Console.WriteLine(@"First line
#line 6
Second line");
```

A #line default directive reverses the effect of all preceding #line directives. The compiler reports true line information for subsequent lines, precisely as if no #line directives had been processed.

A #line hidden directive has no effect on the file and line numbers reported in error messages, but does affect source-level debugging. When debugging, all lines between a #line hidden directive and the subsequent #line directive (that is not #line hidden) have no line number information. When stepping through code in the debugger, these lines will be skipped entirely.

Note that a file-name differs from a regular string literal in that escape characters are not processed; the '\' character simply designates an ordinary backslash character within a file-name.

## 2.5.8 Pragma Directives

The #pragma preprocessing directive is used to specify optional contextual information to the compiler. The information supplied in a #pragma directive will never change program semantics.

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
```

```
pragma-body:
    pragma-warning-body
```

C# provides #pragma directives to control compiler warnings. Future versions of the language may include additional #pragma directives. To ensure interoperability with other C# compilers, the Microsoft C# compiler does not issue compilation errors for unknown #pragma directives; such directives do, however, generate warnings.

### 2.5.8.1 Pragma Warning

The #pragma warning directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
```

```
warning-action:
    disable
    restore
```
