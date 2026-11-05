```
fragment PP_Start
: { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace? // see note below
;

fragment PP_Whitespace
: [ \p{Zs} ] // any character with Unicode class Zs
| '\\u0009' // horizontal tab
| '\\u000C' // form feed
)+
;

fragment PP_New_Line
: PP_Whitespace? Single_Line_Comment? New_Line
;

// Source: $6.5.2 Conditional compilation symbols
fragment PP_Conditional_Symbol
: Basic_Identifier // must not be equal to tokens TRUE or FALSE, see note below
;

// Source: $6.5.3 Pre-processing expressions
fragment PP_Expression
: PP_Whitespace? PP_Or_Expression PP_Whitespace?
;

fragment PP_Or_Expression
: PP_And_Expression (PP_Whitespace? '||' PP_Whitespace? PP_And_Expression)*
;

fragment PP_And_Expression
: PP_Equality_Expression (PP_Whitespace? '&&' PP_Whitespace?
PP_Equality_Expression)*
;

fragment PP_Equality_Expression
: PP_Unary_Expression (PP_Whitespace? ('==' | '!=') PP_Whitespace?
PP_Unary_Expression)*
;

fragment PP_Unary_Expression
: PP_Primary_Expression
| '!' PP_Whitespace? PP_Unary_Expression
;

fragment PP_Primary_Expression
: TRUE
| FALSE
| PP_Conditional_Symbol
| '(' PP_Whitespace? PP_Expression PP_Whitespace? ')'
;

// Source: $6.5.4 Definition directives
fragment PP_Declaration
```