```
```csharp
#endif
}
```
```

results in the exact same sequence of tokens as the program

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

*end example*

# ## 6.5.2 Conditional compilation symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through pre-processing expressions (§6.5.3) and conditional compilation symbols.

```
```csharp
fragment PP_Conditional_Symbol
    : Basic_Identifier // must not be equal to tokens TRUE or FALSE, see note below
    ;
```
```

*Note How an implementation enforces the restriction on the allowable Basic_Identifier values is an implementation issue. end note*

Two conditional compilation symbols are considered the same if they are identical after the following transformations are applied, in order:

+   - Each Unicode_Escape_Sequence is transformed into its corresponding Unicode character.
+   - Any Formatting_Characters are removed.

A conditional compilation symbol has two possible states: defined or undefined. At the beginning of the lexical processing of a compilation unit, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option). When a #define directive is processed, the conditional compilation symbol named in that directive becomes defined in that compilation unit. The symbol remains defined until a #undef directive for that same symbol is processed, or until the end of the compilation unit is reached. An implication of this is that #define and #undef directives in one compilation unit have no effect on other compilation units in the same program.

When referenced in a pre-processing expression (§6.5.3), a defined conditional compilation symbol has the Boolean value true, and an undefined conditional compilation symbol has the Boolean value false. There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in pre-processing expressions. Instead, undeclared symbols are simply undefined and thus have the value false.

The namespace for conditional compilation symbols is distinct and separate from all other named entities in a C# program. Conditional compilation symbols can only be referenced in #define and #undef directives and in pre-processing expressions.

# ## 6.5.3 Pre-processing expressions

Pre-processing expressions can occur in #if and #elif directives. The operators !, ==, !=, &&, and || are permitted in pre-processing expressions, and parentheses may be used for grouping.

```
```csharp
fragment PP_Expression
    : PP_Whitespace? PP_Or_Expression PP_Whitespace?
```
```