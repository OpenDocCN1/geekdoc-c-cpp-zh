© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

returning an int, and (h) array of an unspecified number of constant pointers to functions, each with one parameter that has unsigned int and an unspecified number of other parameters, returning an int.

# ## 6.7.8 Type definitions

Syntax

```
typedef-name:
identifier
```

Constraints

+   1 If a name specifies a variably modified type then it shall have block scope.

Semantics

+   3 In a declaration whose storage-class specifier is typedef, each declarator defines an identifier to be a typedef name that denotes the type specified for the identifier in the way described in 6.7.6. Any array size associated with variable length declarators are evaluated each time the typedef name is reached in the order of execution. A typedef declaration does not introduce a new type, only a synonym for the type specified. That is, in the following declarations:

```
typedef T type_ident;
type_ident D;
```

type_ident is defined as a name with the type specified by the declaration speakers in T (known as T), and the identifier in D has the type "derived-declarator-type-list T" where the derived-declarator-type-list is specified by the declarators of D. A declarator shares the same name as others declared in ordinary declarators.

+   4 EXAMPLE 1 After

```
typedef MILES, KICKSP();
typedef struct { double hi, lo; } range;
```

the constructions

MILES distance;
extern KICKSP *metricsp;
range x;
range z, *zp;

are all valid. The type of distance is int, that of metricsp is "pointer to function with no parameter specification returning "int", and of x and z is the specified structure; zp is a pointer to such a structure. The object distance has a compatible with any other int object.

+   5 EXAMPLE 2 After the declarations

```
typedef struct s { int x; } t1, *tp1;
typedef struct s { int x; } t2, *tp2;
```

t1 and the type pointed to by tp1 are compatible. Type tl is also compatible with struct

$6.7 Language 137