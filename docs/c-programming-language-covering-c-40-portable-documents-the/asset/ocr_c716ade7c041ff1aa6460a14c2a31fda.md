Within the same program, two anonymous object initializers that specify a sequence of properties of the same names and compile-time types in the same order will produce instances of the same anonymous type.

In the example

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

the assignment on the last line is permitted because p1 and p2 are of the same anonymous type.

The Equals and GetHashcode methods on anonymous types override the methods inherited from object, and are defined in terms of the Equals and GetHashcode of the properties, so that two instances of the same anonymous type are equal if and only if all their properties are equal.

A member declarator can be abbreviated to a simple name (§7.5.2), a member access (§7.5.4), or a base access (§7.6.8). This is called a projection initializer and is shorthand for a declaration of and assignment to a property with the same name. Specifically, member declarators of the forms

```
identifier

expr . identifier
```

are precisely equivalent to the following, respectively:

```
identifier = identifier
identifier = expr . identifier
```

Thus, in a projection initializer, the identifier selects both the value and the field or property to which the value is assigned. Intuitively, a projection initializer projects not just a value, but also the name of the value.

# 7.6.11 The typeof Operator

The typeof operator is used to obtain the System.Type object for a type.

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )
```

```
unbound-type-name:
    identifier generic-dimension-specifier_opt
    identifier :: identifier generic-dimension-specifier_opt
    unbound-type-name . identifier generic-dimension-specifier_opt
```