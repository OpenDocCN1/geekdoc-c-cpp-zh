
is true because the two literals refer to the same string instance.

*end example*

### 6.4.5.7 The null literal

```
null_literal
  : NULL
  ;
```

*Note:* null_literal is a parser rule as it does not introduce a new token kind. *end note*

A null_literal represents a null value. It does not have a type, but can be converted to any reference type or nullable value type through a null literal conversion (§10.2.7).

### 6.4.6 Operators and punctuators

There are several kinds of operators and punctuators. Operators are used in expressions to describe operations involving one or more operands.

*Example:* The expression a + b uses the + operator to add the two operands a and b. *end example*

Punctuators are for grouping and separating.

```
operator_or_punctuator
  : '{' | '}' | '[' | ']' | '(' | ')' | '.' | ',' | ':' | ';' | '+' | '-' | ASTERISK | SLASH | '%' | '&' | '|' | '^' | '!' | '~' | '=' | '<' | '>' | '?' | '::' | '++' | '--' | '&&' | '||' | '==' | '!=' | '<=' | '>=' | '??' | ':=' | '+-' | '-+' | '==' | '!=' | '=>' | '&=' | '|=' | '^=' | '<<' | '<<=' | '>>' | '>>=' | '*=' | '/=' | '%=' | '&=' | '|=' | '^=' | '!=' | ...
  ;
```

```
right_shift
  : '>' '>'
  ;
```

```
right_shift_assignment
  : '>' '>='
  ;
```

*Note:* right_shift and right_shift_assignment are parser rules as they do not introduce a new token kind but represent a sequence of two tokens. The operator_or_punctuator rule exists for descriptive purposes only and is not used elsewhere in the grammar. *end note*

right_shift is made up of the two tokens > and >. Similarly, right_shift_assignment is made up of the two tokens > and >=. Unlike other productions in the syntactic grammar, no characters of any kind (not even whitespace) are allowed between the two tokens in each of these productions. These productions are treated specially in order to enable the correct handling of type_parameter_lists (§15.2.3).

*Note:* Prior to the addition of generics to C#, >> and >>= were both single tokens. However, the syntax for generics uses the < and > characters to delimit type parameters and type arguments. It is often desirable to use nested constructed types, such as List<Dictionary<string, int>>. Rather than requiring the programmer to separate the > and > by a space, the definition of the two operator_or_punctuators was changed. *end note*

## 6.5 Pre-processing directives

### 6.5.1 General

The pre-processing directives provide the ability to conditionally skip sections of compilation units, to report error and warning conditions, and to delineate distinct regions of source code.

*Note:* The term “pre-processing directives” is used only for consistency with the C and C++ programming languages. In C#, there is no separate pre-processing step; pre-processing directives are processed as part of the lexical analysis phase. *end note*

```
PP_Directive
  : PP_Start PP_Kind PP_New_Line
  ;
```

```
fragment PP_Kind
  : PP_Declaration
  | PP_Conditional
  | PP_Line
  | PP_Diagnostic
  | PP_Region
  | PP_Pragma
  ;
```

```
// Only recognised at the beginning of a line
fragment PP_Start
  // See note below.
  : { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace?
  ;
```

```
fragment PP_Whitespace
  : ( [\p{Zs}]  // any character with Unicode class Zs
    | '\u0009'  // horizontal tab
    | '\u000B'  // vertical tab
    | '\u000C'  // form feed
    )+
  ;
```

```
fragment PP_New_Line
  : PP_Whitespace? Single_Line_Comment? New_Line
  ;
```

*Note:*

- The pre-processor grammar defines a single lexical token PP_Directive used for all pre-processing directives. The semantics of each of the pre-processing directives are defined in this language specification but not how to implement them.
- The PP_Start fragment must only be recognised at the start of a line, the getCharPositionInLine() == 0 ANTLR lexical predicate above suggests one way in which this may be achieved and is informative only, an implementation may use a different strategy.

*end note*

The following pre-processing directives are available:

- #define and #undef, which are used to define and undefine, respectively, conditional compilation symbols (§6.5.4).
- #if, #elif, #else, and #endif, which are used to skip conditionally sections of source code (§6.5.5).
- #line, which is used to control line numbers emitted for errors and warnings (§6.5.8).
- #error, which is used to issue errors (§6.5.6).
- #region and #endregion, which are used to explicitly mark sections of source code (§6.5.7).
- #pragma, which is used to specify optional contextual information to a compiler (§6.5.9).

A pre-processing directive always occupies a separate line of source code and always begins with a # character and a pre-processing directive name. White space may occur before the # character and between the # character and the directive name.

A source line containing a #define, #undef, #if, #elif, #else, #endif, #line, or #endregion directive can end with a single-line comment. Delimited comments (the /* */ style of comments) are not permitted on source lines containing pre-processing directives.

Pre-processing directives are not part of the syntactic grammar of C#. However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program.

*Example: When compiled, the program*

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

Thus, whereas lexically, the two programs are quite different, syntactically, they are identical.

*end example*

### 6.5.2 Conditional compilation symbols

The conditional compilation functionality provided by the #if, #elif, #else, and #endif directives is controlled through pre-processing expressions (§6.5.3) and conditional compilation symbols.

```
fragment PP_Conditional_Symbol
    // Must not be equal to tokens TRUE or FALSE. See note below.
    : Basic_Identifier
    ;
```

*Note:* How an implementation enforces the restriction on the allowable *Basic_Identifier* values is an implementation issue. *end note*

Two conditional compilation symbols are considered the same if they are identical after the following transformations are applied, in order:

- Each *Unicode_Escape_Sequence* is transformed into its corresponding Unicode character.
- Any *Formatting_Characters* are removed.

A conditional compilation symbol has two possible states: *defined* or *undefined*. At the beginning of the lexical processing of a compilation unit, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option). When a #define directive is processed, the conditional compilation symbol named in that directive becomes defined in that compilation unit. The symbol remains defined until a #undef directive for that same symbol is processed, or until the end of the compilation unit is reached. An implication of this is that #define and #undef directives in one compilation unit have no effect on other compilation units in the same program.

When referenced in a pre-processing expression (§6.5.3), a defined conditional compilation symbol has the Boolean value true, and an undefined conditional compilation symbol has the Boolean value false. There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in pre-processing expressions. Instead, undeclared symbols are simply undefined and thus have the value false.

The namespace for conditional compilation symbols is distinct and separate from all other named entities in a C# program. Conditional compilation symbols can only be referenced in #define and #undef directives and in pre-processing expressions.

### 6.5.3 Pre-processing expressions

Pre-processing expressions can occur in #if and #elif directives. The operators !, ==, !=, &&, and || are permitted in pre-processing expressions, and parentheses may be used for grouping.

```
fragment PP_Expression
    : PP_Whitespace? PP_Or_Expression PP_Whitespace?
    ;

fragment PP_Or_Expression
    : PP_And_Expression (PP_Whitespace? '||' PP_Whitespace? PP_And_Expression)*
    ;

fragment PP_And_Expression
    : PP_Equality_Expression (PP_Whitespace? '&&' PP_Whitespace? PP_Equality_Expression)*
    ;

fragment PP_Equality_Expression
    : PP_Unary_Expression (PP_Whitespace? ('==' | '!=') PP_Whitespace? PP_Unary_Expression)*
    ;

fragment PP_Unary_Expression
```
