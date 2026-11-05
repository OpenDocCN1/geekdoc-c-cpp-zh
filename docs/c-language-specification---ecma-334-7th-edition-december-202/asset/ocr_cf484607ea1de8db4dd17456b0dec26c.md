# 6.5 Pre-processing directives

# 6.5.1 General

The pre-processing directives provide the ability to conditionally skip sections of compilation units, to report error and warning conditions, and to delineate distinct regions of source code.

> *Note:* The term “pre-processing directives” is used only for consistency with the C and C++ programming languages. In C#, there is no separate pre-processing step; pre-processing directives are processed as part of the lexical analysis phase. *end note*

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
  : ( [p{Zs}]  // any character with Unicode class Zs
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

+   - The pre-processor grammar defines a single lexical token PP_Directive used for all pre-processing directives. The semantics of each of the pre-processing directives are defined in this language specification but not how to implement them.
+   - The PP_Start fragment must only be recognised at the start of a line, the getCharPositionInLine() == 0 ANTLR lexical predicate above suggests one way in which this may be achieved and is informative only, an implementation may use a different strategy.

*end note*

The following pre-processing directives are available: