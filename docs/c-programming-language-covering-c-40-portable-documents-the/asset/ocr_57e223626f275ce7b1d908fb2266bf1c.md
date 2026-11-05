A #line default directive reverses the effect of all preceding #line directives. The compiler reports true line information for subsequent lines, precisely as if no #line directives had been processed.

A #line hidden directive has no effect on the file and line numbers reported in error messages, but does affect source-level debugging. When debugging, all lines between a #line hidden directive and the subsequent #line directive (that is not #line hidden) have no line number information. When stepping through code in the debugger, these lines will be skipped entirely.

Note that a file-name differs from a regular string literal in that escape characters are not processed; the '\' character simply designates an ordinary backslash character within a file-name.

# 2.5.8 Pragma Directives

The #pragma preprocessing directive is used to specify optional contextual information to the compiler. The information supplied in a #pragma directive will never change program semantics.

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line

pragma-body:
    pragma-warning-body
```

C# provides #pragma directives to control compiler warnings. Future versions of the language may include additional #pragma directives. To ensure interoperability with other C# compilers, the Microsoft C# compiler does not issue compilation errors for unknown #pragma directives; such directives do, however, generate warnings.

# 2.5.8.1 Pragma Warning

The #pragma warning directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list

warning-action:
    disable
    restore
```