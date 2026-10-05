# 7.1.2 Standard headers

Each library function is declared, with a type that includes a prototype, in a header<sup>182</sup> whose contents are made available by the #include preprocessing directive. The header declares a set of related functions, plus any necessary types and additional macros needed to facilitate their use. Declarations of types described in this clause shall not include type qualifiers, unless explicitly stated otherwise.

The standard headers are<sup>183</sup>

```
<assert.h>          <math.h>           <stdlib.h>
<complex.h>         <setjmp.h>        <stdnorm.h>
<ctype.h>           <signal.h>        <string.h>
<errno.h>           <stdalign.h>      <tgmath.h>
<fenv.h>            <stdarg.h>        <threads.h>
<float.h>           <statomic.h>      <time.h>
<intypes.h>         <stdbool.h>       <uchar.h>
<iso646.h>          <stddef.h>        <wchar.h>
<limits.h>          <stdio.h>
<locale.h>          <stdio.h>\wctype.h>
```

If a file with the same name as one of the above < > delimited sequences, is provided as part of the implementation, is placed in any of the standard places that are searched for source files, the behavior is undefined.

Standard headers may be included in any order; each may be included more than once in a given scope, with no effect different from being only once, except the effect of including <assert.h> depends on the definition of DEBUG (see 7.2). If used, a header shall be included outside of any external declaration or definition, and it shall be included before the first reference to any of the functions or objects it declares, or to any of the types or macros it defines. However, if an identifier is declared or defined in more than one header, the second and subsequent associated headers be included after the initial reference to it. The program shall not have any macros with names lexically identical to keywords defined prior to the inclusion of the header or when any macro defined in the header is expanded.

Any definition of an object-like macro described in this clause shall expand to code that is fully protected by parentheses where necessary, so that it groups in an arbitrary expression as if it were a single identifier.

> 182) A header is not necessarily a source file, nor are the < > delimited sequences in header names necessarily valid source file names.

> 183) The headers <complex.h>, <statomic.h>, and <threads.h> are conditional features that implementations may not support; see 6.10.8.3.