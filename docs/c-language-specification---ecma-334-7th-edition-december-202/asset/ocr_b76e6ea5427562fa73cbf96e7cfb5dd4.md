```
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

// Source: §6.5.4 Definition directives
fragment PP_Declaration
  : 'define' PP_Whitespace PP_Conditional_Symbol
  | 'undef' PP_Whitespace PP_Conditional_Symbol
  ;

// Source: §6.5.5 Conditional compilation directives
fragment PP_Conditional
  : PP_If_Section
  | PP_Elif_Section
  | PP_Else_Section
  | PP_Endif
  ;

fragment PP_If_Section
  : 'if' PP_Whitespace PP_Expression
  ;

fragment PP_Elif_Section
  : 'elif' PP_Whitespace PP_Expression
  ;

fragment PP_Else_Section
  : 'else'
  ;

fragment PP_Endif
  : 'endif'
  ;

// Source: §6.5.6 Diagnostic directives
fragment PP_Diagnostic
```