
The processing of a `#define` directive causes the given conditional compilation symbol to become defined, starting with the source line that follows the directive. Likewise, the processing of a `#undef` directive causes the given conditional compilation symbol to become undefined, starting with the source line that follows the directive.

Any `#define` and `#undef` directives in a source file must occur before the first token (§2.4) in the source file; otherwise, a compile-time error occurs. In intuitive terms, `#define` and `#undef` directives must precede any “real code” in the source file.

The example

```csharp
#define Enterprise
#if Professional || Enterprise
    #define Advanced
#endif

namespace Megacorp.Data
{
    #if Advanced
    class PivotTable {...}
    #endif
}
```

is valid because the `#define` directives precede the first token (the `namespace` keyword) in the source file.

The following example results in a compile-time error because a `#define` follows real code:

```csharp
#define A
namespace N
{
    #define B
    #if B
    class Class1 {}
    #endif
}
```

A `#define` may define a conditional compilation symbol that is already defined, without there being any intervening `#undef` for that symbol. The example below defines a conditional compilation symbol `A` and then defines it again.

```csharp
#define A
#define A
```

A `#undef` may “undefine” a conditional compilation symbol that is not defined. The example below defines a conditional compilation symbol `A` and then undefines it twice; although the second `#undef` has no effect, it is still valid.

```csharp
#define A
#undef A
#undef A
```

## 2.5.4 Conditional Compilation Directives

The conditional compilation directives are used to conditionally include or exclude portions of a source file.

```text
pp-conditional:
  pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
  whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line
  conditional-section_opt

pp-elif-sections
  pp-elif-section
  pp-elif-sections pp-elif-section

pp-elif-section:
  whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line
  conditional-section_opt

pp-else-section:
  whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt

pp-endif:
  whitespace_opt # whitespace_opt endif pp-new-line

conditional-section:
  input-section
  skipped-section

skipped-section:
  skipped-section-part
  skipped-section skipped-section-part

skipped-section-part:
  skipped-characters_opt new-line
  pp-directive

skipped-characters:
  whitespace_opt not-number-sign input-characters_opt

not-number-sign:
  Any input-character except #
```

As indicated by the syntax, conditional compilation directives must be written as sets consisting of, in order, an `#if` directive, zero or more `#elif` directives, zero or one `#else` directive, and an `#endif` directive. Between the directives are conditional sections of source code. Each section is controlled by the immediately preceding directive. A conditional section may itself contain nested conditional compilation directives provided these directives form complete sets.

> **CHRIS SELLS** I can see `#if` and `#endif`, but `#elif`? Is this a Santa’s helper with a lisp? A hipster abbreviation for some large, gray, wrinkled animal? I’d have preferred springing for the two extra characters in `#elseif` simply so I could actually remember it…

A pp-conditional selects at most one of the contained conditional-sections for normal lexical processing:

- The pp-expressions of the `#if` and `#elif` directives are evaluated in order until one yields true. If an expression yields true, the conditional-section of the corresponding directive is selected.
- If all pp-expressions yield false, and if an `#else` directive is present, the conditional-section of the `#else` directive is selected.
- Otherwise, no conditional-section is selected.

The selected conditional-section, if any, is processed as a normal input-section: The source code contained in the section must adhere to the lexical grammar; tokens are generated from the source code in the section; and preprocessing directives in the section have the prescribed effects.

The remaining conditional-sections, if any, are processed as skipped-sections: Except for preprocessing directives, the source code in the section need not adhere to the lexical grammar; no tokens are generated from the source code in the section; and preprocessing directives in the section must be lexically correct but are not otherwise processed. Within a conditional-section that is being processed as a skipped-section, any nested conditional-sections (contained in nested `#if…#endif` and `#region…#endregion` constructs) are also processed as skipped-sections.

The following example illustrates how conditional compilation directives can nest:

```csharp
#define Debug    // Debugging on
#undef Trace    // Tracing off
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

Except for preprocessing directives, skipped source code is not subject to lexical analysis. For example, the following is valid despite the unterminated comment in the `#else` section:

```csharp
#define Debug    // Debugging on
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

> **CHRIS SELLS** Avoid the use of nested preprocessing directives if you can, simply because by default the most popular C# editor on the planet, Visual Studio, will arrange them along the left edge of your text file, making it very difficult to follow the nesting. For example,

```csharp
#define Debug    // Debugging on
#undef Trace    // Tracing off
class PurchaseTransaction
    void Commit() {
#if Debug
    CheckConsistency();
#if Trace
    WriteToLog(this.ToString());
#endif
#endif
    CommitHelper();
}
```

Preprocessing directives are not processed when they appear inside multi-line input elements. For example, the program

```csharp
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

```text
hello,
#if Debug
world
#else
Nebraska
#endif
```

In peculiar cases, the set of preprocessing directives that is processed might depend on the evaluation of the pp-expression. The example

```csharp
#if X
/*
#else
/* */ class Q { }
#endif
```

always produces the same token stream (`class Q { }`), regardless of whether `X` is defined. If `X` is defined, the only processed directives are `#if` and `#endif`, due to the multi-line comment. If `X` is undefined, then three directives (`#if`, `#else`, `#endif`) are part of the directive set.

## 2.5.5 Diagnostic Directives

The diagnostic directives are used to explicitly generate error and warning messages that are reported in the same way as other compile-time errors and warnings.

```text
pp-diagnostic:
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message
```

```text
pp-message:
    new-line
    whitespace input-characters_opt new-line
```

## The example

```csharp
#warning Code review needed before check-in
#if Debug && Retail
#error A build can't be both debug and retail
#endif
class Test (...)
```

always produces a warning ("Code review needed before check-in"), and produces a compile-time error ("A build can't be both debug and retail") if the conditional symbols `Debug` and `Retail` are both defined. Note that a pp-message can contain arbitrary text; specifically, it need not contain well-formed tokens, as shown by the single quote in the word `can't`.

## 2.5.6 Region Directives

The region directives are used to explicitly mark regions of source code.

```text
pp-region:
    pp-start-region conditional-section_opt pp-end-region

pp-start-region:
    whitespace_opt # whitespace_opt region pp-message

pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

No semantic meaning is attached to a region; regions are intended for use by the programmer or by automated tools to mark a section of source code. The message specified in a `#region` or `#endregion` directive likewise has no semantic meaning; it merely serves to identify the region. Matching `#region` and `#endregion` directives may have different pp-messages.

## The lexical processing of a region

```csharp
#region
...
#endregion
```

corresponds exactly to the lexical processing of a conditional compilation directive of the form:

```csharp
#if true
...
#endif
```
