
in the same program, these string literals refer to the same string instance. For instance, the output produced by

```
class Test
{
    static void Main() {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```

is True because the two literals refer to the same string instance.

> JOSEPH ALBAHARI This optimization is called interning. One of the benefits of interning is that it reduces the size of the compiled assembly because duplicate string literals are factored out.

> In the preceding example, a and b are declared of type object, which forces the subsequent comparison to use object's reference-type equality semantics. If a and b were declared of type string, the comparison would bind to string's == operator, which evaluates to true if the strings have identical content—even if they refer to different underlying objects.

### 2.4.4.6 The null Literal

null-literal:
null

The null-literal can be implicitly converted to a reference type or nullable type.

> ERIC LIPPERT The null literal expression itself does not have a type.

## 2.4.5 Operators and Punctuators

There are several kinds of operators and punctuators. Operators are used in expressions to describe operations involving one or more operands. For example, the expression a + b uses the + operator to add the two operands a and b. Punctuators are for grouping and separating.

```
operator-or-punctuator: one of
{ } [ ] ( ) . \ : ; ~
+ - * / % & | , ! ^
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>
```

### right-shift:

```
>|>
```

### right-shift-assignment:

```
>|=>
```

The vertical bars in the right-shift and right-shift-assignment productions are used to indicate that, unlike other productions in the syntactic grammar, no characters of any kind (not even white space) are allowed between the tokens. These productions are treated specially to enable the correct handling of type-parameter-lists (§10.1.3).

## 2.5 Preprocessing Directives

> **BILL WAGNER** This section shows how the C heritage colors so much of modern development. I rarely, if ever, use any of the preprocessing directives—but I can only imagine the storm of criticism if C# had not included a strong set of preprocessing directives.

The preprocessing directives provide the ability to conditionally skip sections of source files, to report error and warning conditions, and to delineate distinct regions of source code. The term “preprocessing directives” is used only for consistency with the C and C++ programming languages. In C#, there is no separate preprocessing step; preprocessing directives are processed as part of the lexical analysis phase.

pp-directive:
- pp-declaration
- pp-conditional
- pp-line
- pp-diagnostic
- pp-region
- pp-pragma

The following preprocessing directives are available:

- #define and #undef, which are used to define and undefine, respectively, conditional compilation symbols (§2.5.3).
- #if, #elif, #else, and #endif, which are used to conditionally skip sections of source code (§2.5.4).
- #line, which is used to control line numbers emitted for errors and warnings (§2.5.7).
- #error and #warning, which are used to issue errors and warnings, respectively (§2.5.5).
- #region and #endregion, which are used to explicitly mark sections of source code (§2.5.6).
- #pragma, which is used to specify optional contextual information to the compiler (§2.5.8).

A preprocessing directive always occupies a separate line of source code and always begins with a # character and a preprocessing directive name. White space may occur before the # character and between the # character and the directive name.

A source line containing a #define, #undef, #if, #elif, #else, #endif, or #line directive may end with a single-line comment. Delimited comments (the /* */ style of comments) are not permitted on source lines containing preprocessing directives.

Preprocessing directives are not tokens and are not part of the syntactic grammar of C#. However, preprocessing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program. For example, when compiled, the program

```
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

results in the exact same sequence of tokens as the program

```
class C
{
    void F() {}
    void I() {}
}
```

Thus, whereas lexically the two programs are quite different, syntactically they are identical.

### 2.5.1 Conditional Compilation Symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through preprocessing expressions (§2.5.2) and conditional compilation symbols.

conditional-symbol:
Any identifier-or-keyword except true or false

A conditional compilation symbol has two possible states: defined or undefined. At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option). When a #define directive is processed, the conditional compilation symbol named in that directive becomes defined in that source file. The symbol remains defined until an #undef directive for that same symbol is processed, or until the end of the source file is reached. An implication of this is that #define and #undef directives in one source file have no effect on other source files in the same program.

When referenced in a preprocessing expression, a defined conditional compilation symbol has the boolean value true, and an undefined conditional compilation symbol has the boolean value false. There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in preprocessing expressions. Instead, undeclared symbols are simply undefined and thus have the value false.

The name space for conditional compilation symbols is distinct and separate from all other named entities in a C# program. Conditional compilation symbols can only be referenced in #define and #undef directives and in preprocessing expressions.

### 2.5.2 Preprocessing Expressions

Preprocessing expressions can occur in #if and #elif directives. The operators !, ==, !=, &&, and || are permitted in preprocessing expressions, and parentheses may be used for grouping.

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

When referenced in a preprocessing expression, a defined conditional compilation symbol has the boolean value true, and an undefined conditional compilation symbol has the boolean value false.

Evaluation of a preprocessing expression always yields a boolean value. The rules of evaluation for a preprocessing expression are the same as those for a constant expression (§7.19), except that the only user-defined entities that can be referenced are conditional compilation symbols.

### 2.5.3 Declaration Directives

The declaration directives are used to define or undefine conditional compilation symbols.

```
pp-declaration:
  whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
  whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

pp-new-line:
  whitespace_opt single-line-comment_opt new-line
```
