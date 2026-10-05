
# Preprocessing directives of the forms

```
# ifdef identifier new-line group_opt
# ifndef identifier new-line group_opt
```

check whether the identifier is not currently defined as a macro name. Their conditions are equivalent to **#if defined identifier** and **#if !defined identifier** respectively.

Each directive's condition is checked in order. If it evaluates to false (zero), the group that it controls is skipped; directives are processed only through the name that determines the directive in order to keep track of the level of nested conditionals; the rest of the directives' preprocessing tokens are ignored, as are the other preprocessing tokens in the group. Only the first group whose control condition evaluates to true (nonzero) is processed. If there is a **#else** directive, the group controlled by the **#else** is processed; lacking a **#else** directive, all the groups until the **#endif** are skipped.¹169)

**Forward references:** macro replacement (6.10.3), source file inclusion (6.10.2), largest integer types (7.20.1.5).

## 6.10.2 Source file inclusion

### Constraints

A **#include** directive shall identify a header or source file that can be processed by the implementation.

### Semantics

A preprocessing directive of the form

```
# include <h-char-sequence> new-line
```

searches a sequence of implementation-defined places for a header identified uniquely by the specified sequence between the **<** and **>** delimiters, and causes the replacement of that directive by the entire contents of the header. How the places are specified or the header identified is implementation-defined.

A preprocessing directive of the form

```
# include "q-char-sequence" new-line
```

causes the replacement of that directive by the entire contents of the source file identified by the specified sequence between the " " delimiters. The named source file is searched for an implementation-defined manner. if this search is not supported, or if the search fails, the directive is reprocessed if it is read

```
# include <h-char-sequence> new-line
```

with the identical contained sequence (including > characters, if any) from the original directive.

> 169) As indicated by the syntax, a preprocessing token shall not follow a **#else or or #endif** directive before the terminating new-line character. However, comments may appear anywhere in a source file, including within a preprocessing directive.

4 A preprocessing directive of the form

```
# include pp-tokens new-line
```

(that does not match one of the two previous forms) is permitted. The preprocessing tokens after include in the directive are processed just as in normal text. (Each identifier clearly defined as a macro is replaced by its replacement list of preprocessing tokens.) The directive resulting after all replacements shall match one of the two previous forms.¹17⁰) The method by which a sequence of preprocessing tokens between a < and a > preprocessing token pair or a pair of " characters is combined into a single header name preprocessing token is implementation-defined.

5 The implementation shall provide unique mappings for sequences consisting of one or more nondigits or digits (6.4.2.1) followed by a period (.) and a single nondigit. The first character shall not be a digit. The implementation may ignore distinctions of alphabetic case and restrict the mapping to eight significant characters before the period.

6 A #include preprocessing directive may appear in a source file that has been read because of a #include directive in another file, up to an implementation-defined nesting limit (see 5.2.4.1).

7 EXAMPLE 1 The most common uses of #include preprocessing directives are as in the following:

```
#include <stdio.h>
#include "myprog.h"
```

EXAMPLE 2 This illustrates macro-replaced #include directives:

```
#if VERSION = 1
  #define INCFILE "vers1.h"
#elif VERSION = 2
  #define INCFILE "vers2.h" // and so on
#else
  #define INCFILE "versN.h"
#endif
#include INCFILE
```

Forward references: macro replacement (6.10.3).

## 6.10.3 Macro replacement

### Constraints

- Two replacement lists are identical if and only if the preprocessing tokens in both have the same number, ordering, spelling, and white-space separation, where all white-space separations are considered identical.
- An identifier currently defined as an object-like macro shall not be redefined by another #define preprocessing directive unless the second definition is an object-like macro definition and the two replacement lists are identical. Likewise, an identifier currently defined as a function-like macro shall not be redefined by another #define preprocessing directive unless the second definition is a function-like macro definition that has the same number and spelling of parameters, and the two replacement lists are identical.
- There shall be white-space between the identifier and the replacement list in the definition of an object-like macro.
- If the identifier-list in the macro definition does not end with an ellipsis, the number of arguments (including those consisting of no preprocessing tokens) in an invocation of a function-like macro shall equal the number of parameters in the macro definition. Otherwise, there shall be more arguments in the invocation than there are parameters in the macro definition (excluding the ...). There shall exist a ) preprocessing token that terminates the invocation.
- The identifier __VA_ARGS__ shall occur only in the replacement-list of a function-like macro that uses the ellipsis notation in the parameters.
- A parameter identifier in a function-like macro shall be uniquely declared within its scope.

### Semantics

- The identifier immediately following the define is called the macro name. There is one name space for macro names. Any white-space characters preceding or following the replacement list are not considered part of the replacement

8 If a preprocessing token, followed by an identifier, occurs lexically at the point at which a preprocessing directive could begin, the identifier is not subject to macro replacement.

9 A preprocessing directive of the form

```
# define identifier replacement-list new-line
```

defines an object-like macro that causes each subsequent instance of the macro name¹¹ to be replaced by the list of preprocessing tokens that constitute the remainder of the directive. The replacement list is then rescanned for more macro names as specified below.

10 A preprocessing directive of the form

```
# define identifier lparen identifier-list-opt ) replacement-list new-line
# define identifier Lparen ... ) replacement-list new-line
# define identifier lparen identifier-list , ... ) replacement-list new-line
```

defines a function-like macro with parameters, which use similar syntactically to a function call. The parameters are specified by the optional list of identifiers, whose scope extends from their declaration until the new-line character terminates the #preprocessing directive followed by a as the next preprocessing token introduces the sequence of preprocessing tokens that is replaced by the replacement list in the definition (invocation of the macro). The replaced sequence of preprocessing tokens is terminated by the matching ) preprocessing token, skipping intervening pairs of left and right parenthesis tokens.

11 The sequence of preprocessing tokens bounded by the outside-most matching parentheses forms the list of arguments for the function-like macro. The individuals within the list are separated by preprocessing tokens, but comma preprocessing tokens between matching inner parentheses do not separate arguments. If there are sequences of preprocessing directives¹² the behavior is undefined.

12 If there is a ... in the identifier-list in macro definition, the trailing arguments, including any separating comma preprocessing tokens, are merged to a single item:

> 171) Since, by macro-replacement time, all character and string literals are preprocessing tokens, not sequences possibly containing identifier-like subsequences (see 5.1.1.2, translation phases), they are never rescanned for macro names or parameters.

> 172) Despite the name, a non-directive is a preprocessing directive.
