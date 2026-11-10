![](bbox=[0.345, 0.175, 0.64, 0.302])

Figure 4.57: Creating an input/output translator with Yacc

```
```
declarations
%%
translation rules
%%
supporting C routines
```
```

**Example 4.69:** To illustrate how to prepare a Yacc source program, let us construct a simple desk calculator that reads an arithmetic expression, evaluates it, and then prints its numeric value. We shall build the desk calculator starting with the following grammar for arithmetic expressions:

```
```
E → E + T | T
T → T * F | F
F → ( E ) | digit
```
```

The token `digit` is a single digit between 0 and 9. A Yacc desk calculator program derived from this grammar is shown in Fig. 4.58. □

# ### The Declarations Part

There are two sections in the declarations part of a Yacc program; both are optional. In the first section, we put ordinary C declarations, delimited by `%{` and `%}`. Here we place declarations of any temporaries used by the translation rules or procedures of the second and third sections. In Fig. 4.58, this section contains only the include-statement

```
```c
#include <ctype.h>
```
```

that causes the C preprocessor to include the standard header file `<ctype.h>` that contains the predicate `isdigit`.
Also in the declarations part are declarations of grammar tokens. In Fig. 4.58, the statement

```
```yacc
%token DIGIT
```
```