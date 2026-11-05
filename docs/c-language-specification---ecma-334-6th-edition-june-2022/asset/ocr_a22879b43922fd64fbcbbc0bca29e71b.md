```
fragment PP_Line_Indicator
  : Decimal_Digit+ PP_Whitespace PP_Compilation_Unit_Name
  | Decimal_Digit+
  | DEFAULT
  | 'hidden'
  ;

fragment PP_Compilation_Unit_Name
  : '"' PP_Compilation_Unit_Name_Character+ '"'
  ;

fragment PP_Compilation_Unit_Name_Character
  // Any Input_Character except "
  : ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029' | '#')
  ;
```

When no #line directives are present, the compiler reports true line numbers and compilation unit names in its output. When processing a #line directive that includes a Line_Indicator that is not default, the compiler treats the line after the directive as having the given line number (and compilation unit name, if specified).

A #line default directive undoes the effect of all preceding #line directives. The compiler reports true line information for subsequent lines, precisely as if no #line directives had been processed.

A #line hidden directive has no effect on the compilation unit and line numbers reported in error messages, or produced by use of CallerLineNumberAttribute (§21.5.5.2). It is intended to affect source-level debugging tools so that, when debugging, all lines between a #line hidden directive and the subsequent #line directive (that is not #line hidden) have no line number information, and are skipped entirely when stepping through code.

> Note: Although a Compilation_Unit_Name might contain text that looks like an escape sequence, such text is not an escape sequence; in this context a '\' character simply designates an ordinary backslash character. end note

# 6.5.9 Pragma directives

The #pragma preprocessing directive is used to specify contextual information to a compiler.

Note: For example, a compiler might provide #pragma directives that

+   - Enable or disable particular warning messages when compiling subsequent code.
+   - Specify which optimizations to apply to subsequent code.
+   - Specify information to be used by a debugger.

end note

```
fragment PP_Pragma
  : 'pragma' PP_Pragma_Text?
  ;

fragment PP_Pragma_Text
  : PP_Whitespace Input_Character*
  ;
```