If the definition of an object has an alignment specifier, any other declaration of that object should either have an alignment specifier or have no alignment specifier. If the definition of an object does not have an alignment specifier, any other declaration of that object should also have no alignment specifier. If declarations of an object in different translation units have different alignment specifiers, the behavior is undefined.

# 6.7.6 Declarators

Syntax

```
declarator:
    pointer_opt direct-declarator
direct-declarator:
    identifier
    ( declarator )
    direct-declarator [ type-qualifier-list_opt assignment-expression-opt ]
    direct-declarator [ static type-qualifier-list_opt assignment-expression ]
direct-declarator [ type-qualifier-list static assignment-expression ]
direct-declarator [ type-qualifier-list_opt * ]
direct-declarator ( parameter-type-list )
direct-declarator ( identifier-list_opt )

pointer:
    * type-qualifier-list_opt
    * type-qualifier-list_opt pointer
type-qualifier-list:
    type-qualifier
    type-qualifier-list type-qualifier
parameter-type-list:
    parameter-list
    parameter-list , ...
parameter-list:
    parameter-declaration
    parameter-list , parameter-declaration
parameter-declaration:
    declaration-specifiers declarator
    declaration-specifiers abstract-declarator_opt
```

141) An alignment specification of zero also does not affect other alignment specifications in the same declaration.