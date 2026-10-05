# 6.7.9 Initialization

# Syntax

```
initializer:
    assignment-expression
    { initializer-list }
    { initializer-list , }
ninitializer-list:
    designation_opt initializer
    initializer-list , designation_opt initializer
designation:
    designator-list =
designator-list:
    designator
    designator-list designator
designator:
    [ constant-expression ]
    . identifier
```

# Constraints

No initializer shall attempt to provide a value for an object not contained within the entity being initialized.

The type of the entity to be initialized shall be an array of unknown size or a complete object type that is not a variable length array type.

All the expressions in an initializer for an object that has static or thread storage duration shall be constant expressions or string literals.

If the declaration of an identifier has block scope, and the identifier has external or internal linkage, the declaration shall have no initializer for the identifier.

If a designator has a form

```
[ constant-expression ]
```

then the current object (defined below) shall have array type and the expression shall be an integer constant expression. If the array is of unknown size, any nonnegative value is valid.

If a designator has the form

```
. identifier
```

then the current object (defined below) shall have structure or union type and the identifier shall be the name of a member of that type.