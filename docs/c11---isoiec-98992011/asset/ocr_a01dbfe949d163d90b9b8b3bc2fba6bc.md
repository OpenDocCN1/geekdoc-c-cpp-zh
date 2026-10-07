# Semantics

3 If, in the declaration `type-type-list_opt,DI` has one of the forms:

```
D[ type-qualifier-list_opt assignment-expression_opt ]
D[ static type-qualifier-list_opt assignment-expression ]
D[ type-qualifier-list_opt static assignment-expression ]
D[ type-qualifier-list_opt * ]
```

and the type specified for ident in the declaration “D” is `derived-declarator-type-list T”`, then the type specified for ident is `derived-declarator-type array of T`.¹142 (See 6.7.6.3 for the meaning of the optional type qualifiers and the keyword `static`.)

4 If the size is not set, the array type is an incomplete type. If the size is * instead of being an expression, the array type is a variable length array of unspecified size, which can only be used in declarations or type names with function prototype scope;¹143 such arrays are nevertheless complete types. If the size is an integer constant expression and the element type is not a variable length array; otherwise, the array is a variable length array. (Variable length arrays are a conditional feature that implementations may not support; see 6.10.8.3.)

5 If the size is an expression that is not an integer constant expression: if it occurs in a declaration at function prototype scope, it is treated as if it were replaced by */; otherwise, each time it is evaluated it should have a value greater than zero. The size of each variable length array type does not change during lifetime. A size expression is part of the operand of a `sizeof` operator and changing the value of the size expression would not affect the result of the operator, and it is unspecified or not the size expression is evaluated.

6 For two types to be compatible, both should have compatible element types, and if both size specifiers are present, and are integer constant expressions, then both size specifiers are used in a context which requires them to be compatible, it is undefined behavior if the two size specifiers evaluate to unequal values.

7 EXAMPLE 1

```
float a[11], *afp[17];
```

declares an array of `float` numbers and an array of pointers to `float` numbers.

8 EXAMPLE 2 Note the distinction between the declarations

142) When several “array of” specifications are adjacent, a multidimensional array is declared.

143) Thus, * is used only in function declarations that are not definitions (see 6.7.6.3).

| $6.7.6.2 | Language | 131 |