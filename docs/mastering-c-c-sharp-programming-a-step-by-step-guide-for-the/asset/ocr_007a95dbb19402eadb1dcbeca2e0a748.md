For all the other types, the result will be implementation-defined and it is a value and not a constant.

The order that members get packed into a struct is not specified.

For the purpose of alignment, the start, the middle, and the end of a struct may have unnamed padding. The bits that are used as padding are of indeterminate content.

When you apply this to an operand of struct type, the result will be the total bytes on a variable of that specified type and that includes the padding.

# The Fixed Statement

In the unsafe context, embedded_statement production allows for the fixed statement, which is another construct used to fix moveable variables temporarily. This will allow the address of the variable to stay constant throughout the life of the statement.

```
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')'
    embedded_statement
    ;
```

```
fixed_pointer_declarators
    : fixed_pointer_declarator (',' fixed_pointer_declarator)*
    ;
```

```
fixed_pointer_declarator
    : identifier '=' fixed_pointer_initializer
    ;
```

```
fixed_pointer_initializer
```