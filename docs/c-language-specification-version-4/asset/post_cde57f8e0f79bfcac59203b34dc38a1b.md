
The following pre-processing directives are available:

- `#define` and `#undef`, which are used to define and undefine, respectively, conditional compilation symbols (§2.5.3).
- `#if`, `#elif`, `#else`, and `#endif`, which are used to conditionally skip sections of source code (§2.5.4).
- `#line`, which is used to control line numbers emitted for errors and warnings (§2.5.7).
- `#error` and `#warning`, which are used to issue errors and warnings, respectively (§2.5.5).
- `#region` and `#endregion`, which are used to explicitly mark sections of source code (§2.5.6).
- `#pragma`, which is used to specify optional contextual information to the compiler (§2.5.8).

A pre-processing directive always occupies a separate line of source code and always begins with a # character and a pre-processing directive name. White space may occur before the # character and between the # character and the directive name.

A source line containing a #define, #undef, #if, #elif, #else, #endif, or #line directive may end with a single-line comment. Delimited comments (the /* */ style of comments) are not permitted on source lines containing pre-processing directives.

Pre-processing directives are not tokens and are not part of the syntactic grammar of C#. However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program. For example, when compiled, the program:

```csharp
#define A
#undef B

class C
{
#if A
    void F() {}
#else
    void G() {}
#endif

#if B
    void H() {}
#else
    void I() {}
#endif
}
```

results in the exact same sequence of tokens as the program:

```csharp
class C
{
    void F() {}
    void I() {}
}
```

Thus, whereas lexically, the two programs are quite different, syntactically, they are identical.

## 2.5.1 Conditional compilation symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through pre-processing expressions (§2.5.2) and conditional compilation symbols.

```
conditional-symbol:
    Any identifier-or-keyword except true or false
```

A conditional compilation symbol has two possible states: **defined** or **undefined**. At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option). When a #define directive is processed, the conditional compilation symbol named in that directive becomes defined in that source file. The symbol remains defined until an #undef directive for that same symbol is processed, or until the end of the source file is reached. An implication of this is that #define and #undef directives in one source file have no effect on other source files in the same program.

When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value true, and an undefined conditional compilation symbol has the boolean value false. There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in pre-processing expressions. Instead, undeclared symbols are simply undefined and thus have the value false.

The namespace for conditional compilation symbols is distinct and separate from all other named entities in a C# program. Conditional compilation symbols can only be referenced in #define and #undef directives and in pre-processing expressions.

## 2.5.2 Pre-processing expressions

Pre-processing expressions can occur in #if and #elif directives. The operators !, ==, !=, && and || are permitted in pre-processing expressions, and parentheses may be used for grouping.

```
pp-expression:
    whitespace_opt pp-or-expression whitespace_opt

pp-or-expression:
    pp-and-expression
    pp-or-expression whitespace_opt || whitespace_opt pp-and-expression

pp-and-expression:
    pp-equality-expression
    pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression

pp-equality-expression:
    pp-unary-expression
    pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
    pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression

pp-unary-expression:
    pp-primary-expression
    ! whitespace_opt pp-unary-expression

pp-primary-expression:
    true
    false
    conditional-symbol
    ( whitespace_opt pp-expression whitespace_opt )
```

When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value true, and an undefined conditional compilation symbol has the boolean value false.

Evaluation of a pre-processing expression always yields a boolean value. The rules of evaluation for a pre-processing expression are the same as those for a constant expression (§7.19), except that the only user-defined entities that can be referenced are conditional compilation symbols.

## 2.5.3 Declaration directives

The declaration directives are used to define or undefine conditional compilation symbols.

```
pp-declaration:
  whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
  whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

pp-new-line:
  whitespace_opt single-line-comment_opt new-line
```

The processing of a #define directive causes the given conditional compilation symbol to become defined, starting with the source line that follows the directive. Likewise, the processing of an #undef directive causes the given conditional compilation symbol to become undefined, starting with the source line that follows the directive.

Any #define and #undef directives in a source file must occur before the first token (§2.4) in the source file; otherwise a compile-time error occurs. In intuitive terms, #define and #undef directives must precede any “real code” in the source file.

The example:

```
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

is valid because the #define directives precede the first token (the namespace keyword) in the source file.

The following example results in a compile-time error because a #define follows real code:

```
#define A
namespace N
{
  #define B
  #if B
  class Class1 {}
  #endif
}
```

## 2.5.4 Conditional compilation directives

The conditional compilation directives are used to conditionally include or exclude portions of a source file.

```
pp-conditional:
  pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line conditional-section_opt
pp-elif-sections:
    pp-elif-section
    pp-elif-sections pp-elif-section
pp-elif-section:
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line conditional-section_opt
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

As indicated by the syntax, conditional compilation directives must be written as sets consisting of, in order, an #if directive, zero or more #elif directives, zero or one #else directive, and an #endif directive. Between the directives are conditional sections of source code. Each section is controlled by the immediately preceding directive. A conditional section may itself contain nested conditional compilation directives provided these directives form complete sets.

A pp-conditional selects at most one of the contained conditional-sections for normal lexical processing:

- The pp-expressions of the #if and #elif directives are evaluated in order until one yields true. If an expression yields true, the conditional-section of the corresponding directive is selected.
- If all pp-expressions yield false, and if an #else directive is present, the conditional-section of the #else directive is selected.
- Otherwise, no conditional-section is selected.

The selected conditional-section, if any, is processed as a normal input-section: the source code contained in the section must adhere to the lexical grammar; tokens are generated from the source code in the section; and pre-processing directives in the section have the prescribed effects.

The remaining conditional-sections, if any, are processed as skipped-sections: except for pre-processing directives, the source code in the section need not adhere to the lexical grammar; no tokens are generated from the source code in the section; and pre-processing directives in the section must be lexically correct but are not
