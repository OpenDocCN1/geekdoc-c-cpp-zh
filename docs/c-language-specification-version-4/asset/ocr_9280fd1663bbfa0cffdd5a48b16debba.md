The following pre-processing directives are available:

+   - #define and #undef, which are used to define and undefine, respectively, conditional compilation symbols (§2.5.3).
+   - #if, #elif, #else, and #endif, which are used to conditionally skip sections of source code (§2.5.4).
+   - #line, which is used to control line numbers emitted for errors and warnings (§2.5.7).
+   - #error and #warning, which are used to issue errors and warnings, respectively (§2.5.5).
+   - #region and #endregion, which are used to explicitly mark sections of source code (§2.5.6).
+   - #pragma, which is used to specify optional contextual information to the compiler (§2.5.8).

A pre-processing directive always occupies a separate line of source code and always begins with a # character and a pre-processing directive name. White space may occur before the # character and between the # character and the directive name.

A source line containing a #define, #undef, #if, #elif, #else, #endif, or #line directive may end with a single-line comment. Delimited comments (the /* */ style of comments) are not permitted on source lines containing pre-processing directives.

Pre-processing directives are not tokens and are not part of the syntactic grammar of C#. However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program. For example, when compiled, the program:

```
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
```

results in the exact same sequence of tokens as the program:

```
```csharp
class C
{
    void F() {}
    void I() {}
}
```
```

Thus, whereas lexically, the two programs are quite different, syntactically, they are identical.

# 2.5.1 Conditional compilation symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through pre-processing expressions (§2.5.2) and conditional compilation symbols.

conditional-symbol:
    Any identifier-or-keyword except true or false

A conditional compilation symbol has two possible states: **defined** or **undefined**. At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined