# ISO/IEC 9899:2011 (E) © ISO/IEC 2011 – All rights reserved

4 If the input stream has been parsed into preprocessing tokens to a given character, the next preprocessing token is the longest sequence of characters that could constitute a preprocessing token. There is one exception to this rule: header name preprocessing tokens are recognized only within #include preprocessing directives and in implementation-defined locations within #pragma directives. In such contexts, a sequence of characters that could be either a header name or a string literal is recognized as the former.

5 EXAMPLE 1 The program fragment 1 is parsed as a preprocessing number 1 even though the pair of preprocessing tokens 1 and Ex might produce a value expression (for example, if Ex a macro defined as +1). Similarly, the program fragment I1 is parsed as a preprocessing number (one is a valid floating constant), whether not E is a macro name.

6 EXAMPLE 2 The program fragment x++++y is parsed as x + + + + + y, which violates a constraint on increment operators, even though x + + + + y might yield a correct expression.

Forward references: character constants (6.4.4), comments (6.4.9), expressions (6.4.5), floating constants (6.4.4.2), header names (6.4.7), macro replacement (6.10.3), postfix increment and decrement operators (6.5.2.4), prefix increment and decrement operators (6.5.3.1), preprocessing directives (6.10), preprocessing numbers (6.4.8), string literals (6.4.5).

# 6.4.1 Keywords

Syntax keyword: one of

```
auto unsigned
break inline
case void
int volatile
char long while
const register _Alignas
continue restrict _Alignof
default return _Atomic
do short _Bool
double signed _Complex
else sizeof _Generic
enum static _Imaginary
extern struct _Noreturn
float switch _Static_assert
for typedef _Thread_local
goto union
```

Semantics The tokens (case sensitive) are recognized (in translation phases 7 and 8) for use as keywords, and should not be used otherwise. The keyword _Imaginary is reserved for

Language §6.4.1