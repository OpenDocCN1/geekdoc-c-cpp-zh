# Semantics

+   identifier-list:
identifier
identifier-list , identifier

Each declarator declares one identifier, and asserts that when an operand of the same form as the declarator appears in an expression, designates a function or object with the scope, storage duration, and type indicated by the declaration specifiers.

A full declarator is a declarator that is not part of another declarator. The end of a full declarator is a sequence point. If, in the nested sequence of declarators in a full declarator, there is a declarator specifying a variable length array type, the type specified by the full declarator is said to be variably modified. Furthermore, any type derived by the declarator type derivation from a variably modified type is itself variably modified.

In the following subclauses, consider a declaration

# T D1

where T contains the declarator specifiers that specify a T (such as int) and D1 is a declarator that contains an identifier ident. The type specified for the identifier ident in the various forms of declarator is described inductively using this notation.

If, in declaration “T D1”, D1 has the form

identifier

then the type specified for ident is T.

If, in declaration “T D1”, D1 has the form

( D )

then the type specified by the declaration “T D”. Thus, a declarator in parentheses is identical to the unparenthesized declarator, but the binding of complicated declarators may be altered by parentheses.

# Implementation limits

As discussed in 5.2.4.1, an implementation may limit the number of pointer, array, and function declarators that modify an arithmetic, structure, union, or void type, either directly by one or more typedefs.

Forward references: array declarators (6.7.6.2), type definitions (6.7.8).