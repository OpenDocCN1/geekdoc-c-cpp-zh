+   - #if, #elif, #else, and #endif, which are used to skip conditionally sections of source code (§7.5.5).
+   - #line, which is used to control line numbers emitted for errors and warnings (§7.5.8).
+   - #error, which is used to issue errors (§7.5.6).
+   - #region and #endregion, which are used to explicitly mark sections of source code (§7.5.7).
+   - #pragma, which is used to specify optional contextual information to a compiler (§7.5.9).

A pre-processing directive always occupies a separate line of source code and always begins with a # character and a pre-processing directive name. White space may occur before the # character and between the # character and the directive name.

A source line containing a #define, #undef, #if, #elif, #else, #endif, #line, or #endregion directive can end with a single-line comment. Delimited comments (the /* */ style of comments) are not permitted on source lines containing pre-processing directives.

Pre-processing directives are not tokens and are not part of the syntactic grammar of C#. However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program. [Example: When compiled, the program

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

Thus, whereas lexically, the two programs are quite different, syntactically, they are identical. end example]

# 7.5.2 Conditional compilation symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through pre-processing expressions (§7.5.3) and conditional compilation symbols.

conditional-symbol::
Any identifier-or-keyword except true or false

Two conditional compilation symbols are considered the same if they are identical after the following transformations are applied, in order:

+   - Each unicode-escape-sequence is transformed into its corresponding Unicode character.
+   - Any formatting-characters are removed.

A conditional compilation symbol has two possible states: defined or undefined. At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option). When a #define directive is processed, the conditional compilation symbol named in that directive becomes defined in that