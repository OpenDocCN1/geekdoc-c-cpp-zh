© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

# Constraints

A generic selection shall have no more than one default generic association. The type name in a generic association shall specify a complete object other than a variably modified type. No two generic associations in the same generic selection shall specify compatible types. The controlling expression of a generic selection shall have type compatible with at most one of the types named in its generic association list. If a generic selection has no default generic association, its controlling expression shall have type compatible with exactly one of the types named in its generic association.

# Semantics

The controlling expression of a generic selection is not evaluated. If a generic selection has a generic association with a type name that is compatible with the type of the controlling expression, then the result expression of the generic selection is the expression in that generic association. Otherwise, the result expression of the generic selection is the expression in the default generic association. None of the expressions from any other generic association of the generic selection is evaluated.

The type and value of a generic selection are identical to those of its result expression. It is an Invalue, a function descriptor, or a void expression if its result expression is, respectively, Invalue, a function descriptor, or a void expression.

+   EXAMPLE The cbrt type-generic macro could be implemented as:

```
#define cbrt (X) _Generic(X, \
double: cbrtl, \
default: cbrt, \
float: cbrtf \
) (X)
```

# 6.5.2 Postfix operators

# Syntax

```
postfix-expression:
  primary-expression
  postfix-expression [ expression ]
  postfix-expression ( argument-expression-list_opt )
  postfix-expression . identifier
  postfix-expression -> identifier
  postfix-expression ++
  postfix-expression --
  ( type-name ) { initializer-list }
  ( type-name ) { initializer-list , }
```

§6.5.2 Language 79