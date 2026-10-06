# ISO/IEC 14882:2017(E)

a function-like macro (see below) may be redefined by another #define preprocessing directive provided that the second definition is a function-like macro definition that has the same number and spelling of parameters, and the two replacements are identical, otherwise the program is ill-formed.

There will be white-space between the identifier and the replacement list in the definition of an object-like macro.

If the identifier-list in the macro definition does not end with an ellipsis, number of arguments (including those arguments consisting of no preprocessing tokens) in an invocation of a function-like macro shall equal the number of parameters in the macro definition. Otherwise, there shall be more arguments in the invocation than parameters in the macro definition (excluding the ...). There shall exist a ) token that terminates the invocation.

The identifier, VA_ARGS__, shall occur only in the replacement-list of a function-like macro that uses the ellipsis in the parameters.

A identifier in a function-like macro shall be uniquely declared within its scope.

The identifier immediately followed by the defining is the macro name. There is no space for macro names. White-space characters preceding or following the replacement list of preprocessing tokens are not considered part of the replacement list for either form of macro.

If a preprocessing occurs at the point at which a preprocessing directive could be, the identifier is not subject to macro replacement.

+   A preprocessing directive of the form

+   # identifier replacement-list-new-line

an object-like macro that causes each subsequent instance of the macro name¹148 to be replaced by the replacement-list of preprocessing tokens that constitute the remainder of the directive.¹149 The list is then repeated for more macro names as specified:

+   A preprocessing directive of the form

```
# identifier identifier-list( ... ) replacement-list-new-line
# identifier identifier( ... ) replacement-list-new-line
```

a function-like macro with parameters, which use similarly to a function call. The parameters are specified by the optional list of identifiers, whose scope extends from their declaration in the identifier list until the function-like macro name terminates the #preprocessing directive. Each subsequent instance of the function-like macro name followed by a (as the next preprocessing token introduces the sequence of preprocessing tokens it is replaced in the definition of the invocation of the macro). The replaced sequence of preprocessing tokens is terminated by the ) preprocessing token, skipping intervening pairs of left and right preprocessing tokens. The sequence of preprocessing tokens making up an invocation of a function-like macro, new-line is considered

normal white-space character.

The sequence of preprocessing tokens bounded by the outside-most parentheses forms the list of arguments for the function-like macro. The individual identifiers within the list are separated by preprocessing tokens, comma preprocessing tokens between matching identifier parentheses do not separate arguments that would otherwise act as preprocessing directives.¹150 The behavior is undefined.

148) By macro-replacement time, all characters and string literals are preprocessing tokens, sequences not containing identifier-like subsequences (see 5.2, translation phases), are never scanned for macro names or parameters.
an alternative token (3.5) is not an identifier, even when its spelling consists of letters and underscores. Therefore it is not possible to define a macro whose name is the same as that of an alternative token.
150) A conditionally-supported-directive is a preprocessing directive regardless of whether the implementation supports it.