```
: 'define' PP_Whitespace PP_Conditional_Symbol
| 'undef' PP_Whitespace PP_Conditional_Symbol
;

// Source: $6.5.5 Conditional compilation directives
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

// Source: $6.5.6 Diagnostic directives
fragment PP_Diagnostic
  : 'error' PP_Message?
  | 'warning' PP_Message?
  ;

fragment PP_Message
  : PP_Whitespace Input_Character*
  ;

// Source: $6.5.7 Region directives
fragment PP_Region
  : PP_Start_Region
  | PP_End_Region
  ;

fragment PP_Start_Region
  : 'region' PP_Message?
  ;

fragment PP_End_Region
  : 'endregion' PP_Message?
  ;

// Source: $6.5.8 Line directives
fragment PP_Line
  : 'line' PP_Whitespace PP_Line_Indicator
```