
# ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – All rights reserved

(Note that the last declaration also specifies that the argument corresponding to a in any call to f must be a non-null pointer to the first of at least three arrays of 5 doubles, which the others do not.)

**Forward references:** function definitions (6.9.1), type names (6.7.7).

## 6.7.7 Type names

### Syntax

```
type-name:
  specifier-qualifier-list abstract-declarator_opt
  abstract-declarator:
    pointer
      pointer_opt direct-abstract-declarator
  direct-declarator:
    ( abstract-declarator )
    direct-declarator_opt [ type-qualifier-list_opt
      assignment_expression_opt ]
    direct-declarator_opt [ static type-qualifier-list_opt
      assignment_expression ]
    direct-declarator_opt [ type-qualifier-list static
      assignment_expression ]
    direct-declarator_opt [ * ]
    direct-declarator_opt [ parameter-type-list_opt ]
```

### Semantics

In several contexts, it is necessary to specify a type. This is accomplished using a type name, which is syntactically a declaration for a function or an object of that type that omits the identifier.¹⁴⁷ constructions

```
(a) int
(b) int *
(c) int *[3]
(d) int (*)[3]
(e) int (*)
(f) int (*)
(g) int (void)
(h) int (*const [] ) unsigned int, ...
```

name types themselves (a) int, (b) pointer to int, (c) array of pointers to int, (d) pointer to an array of three ints, (e) pointer to a variable length array of an unspecified int, (f) function with no parameter specification returning a pointer to int, (g) pointer to function with parameters returning an int, and (h) array of an unspecified number of constant pointers to functions, each with one parameter that has unsigned int and an unspecified number of other parameters, returning an int.

> ¹⁴⁷ As indicated by the syntax, empty parentheses in a name are interpreted as “function with no parameter specification”, rather than redundant parentheses around the omitted identifier.

## 6.7.8 Type definitions

### Syntax

```
typedef-name:
identifier
```

### Constraints

- 1 If a name specifies a variably modified type then it shall have block scope.

### Semantics

- 3 In a declaration whose storage-class specifier is typedef, each declarator defines an identifier to be a typedef name that denotes the type specified for the identifier in the way described in 6.7.6. Any array size associated with variable length declarators are evaluated each time the typedef name is reached in the order of execution. A typedef declaration does not introduce a new type, only a synonym for the type specified. That is, in the following declarations:

```
typedef T type_ident;
type_ident D;
```

type_ident is defined as a name with the type specified by the declaration speakers in T (known as T), and the identifier in D has the type "derived-declarator-type-list T" where the derived-declarator-type-list is specified by the declarators of D. A declarator shares the same name as others declared in ordinary declarators.

- 4 EXAMPLE 1 After

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

- 5 EXAMPLE 2 After the declarations

```
typedef struct s { int x; } t1, *tp1;
typedef struct s { int x; } t2, *tp2;
```

t1 and the type pointed to by tp1 are compatible. Type t1 is also compatible with struct s1, but not compatible with the types struct s2, t2, the type pointed to by tp2, or int.

EXAMPLE 3 The following obtrusive constructions

```
typedef signed int;
typedef int plain;
struct {
    unsigned t:4;
    const t:5;
    plain r:5;
};
```

declare a type n with type signed int, a name plain with type int, and a structure with three bit-field members, one named t that contains values in the range [0, 15], an unnamed qualified-bit field (if it could be accessed) would contain values in the range [-15, +15] or [-16, +15], and one named r that contains values in the range of [0, 31], [-15, +15], or [-16, +15]. (The choice of range is implementation-defined). The first two bit-field declarations differ in that unsigned is a type qualifier (which forces t to be the name of structure member), while const is a type qualifier (which modifies t is still a valid type). If these declarations are followed in an inner scope

```
long f (t (t));
```

then a function f is declared with "function returning signed int with one unnamed parameter with pointer to signed int with one unnamed parameter with type signed int", an identifier t with long. EXAMPLE 4 On the other hand, named types can be used to improve readability. All three of the following declarations specify exactly the same type, the first without use of any names.

```
typedef void f(int), (*f)(int);
void (*f)(int, void)(int);
void (*f)(int, void);
```

EXAMPLE 5 If a typedef name denotes a variable array type, the length of the array is fixed at the time the typedef name is defined, not each time it is used:

```
void copy(int)
{
    typedef int B[n]; // B is int, evaluated now
    int n = 1; // a and b are different sizes
    int b[n]; // b
    for (int i = 1; i < n; i++)
        a[i] = b[i];
}
```

## 6.7.9 Initialization

### Syntax

```
initializer:
    assignment-expression
    { initializer-list }
initializer-list:
    designation_opt initializer
    { }
designation:
    designator-list =
    designator
    designator-list
designator:
    [ constant-expression ]
    identifier
```

- 2 No initializer shall attempt to provide a value for an object not contained within the entity being initialized.
- 3 The type of the entity to be initialized shall be an array of unknown size or a complete object type that is not variable length array type.
- 4 All the expressions in an initializer for an object that has static or thread duration shall be constant expressions or string literals.
- 5 If the declaration of an identifier has block scope, and the identifier has external or internal linkage, the declaration shall have no identifier for the.
- 6 If a designator has the form [ constant-expression ] then the current object (defined below) shall have array type and the expression shall be an integer expression. If the array is of unknown size, any nonnegative value is valid.
- 7 If a designator has the form .identifier then the current object (defined below) shall have structure or union type and the identifier shall be the name of a member of type.

### Semantics

- 8 An initializer specifies the initial value stored in an object.
- 9 Except where explicitly stated otherwise, for the purposes of this subclause unnamed members of structure and union type do not participate in initialization. Unnamed members of structure objects have indeterminate value even after initialization.
- 10 If an object has automatic storage duration is not initialized explicitly, its value is indeterminate. If an object has static or thread duration is not initialized explicitly, then:
  * if it has pointer type, it is initialized to a null pointer;
  * if it has arithmetic type, it is initialized to (positive or unsigned) zero;
  * if it is an aggregate, every member is initialized (recursively) according to these rules, and any padding is initialized to zero bits;
  * if it is a union, the first member is initialized (recursively) according to these rules, and any padding is initialized to zero bits;
- 11 The initializer for a scalar shall be a expression, optionally enclosed in braces. The initial value of the object is that of the expression (after conversion); the same type constraints and conversions as for simple assignment value, taking the type of the scalar to the unqualified version of its declared type.
- 12 The rest of this subclause deals with initializers for objects that have aggregate or union type.
- 13 The initializer for a structure or union object that has automatic storage duration shall be either an initializer as described below, or a single expression that has compatible structure or union type. In the latter case, the initial value of the object, including unnamed members, is that of the expression.
- 14 An array of character type may be initialized by a character string literal or UTF-8 string literal, optionally enclosed in braces. Successive bytes of the string literal (including the terminating null if there is room or if the array is of unknown size) initialize the elements of the array.
- 15 An array with element type compatible with a qualified or unsigned version of wchar_char16_t or char32_t may be initialized by a wide string literal with the corresponding encoding prefix (L, l, or U, respectively), optionally enclosed in braces. Successive members of the wide string literal (including the terminating null where there is room or if the array is of unknown size) initialize the elements of the array.
- 16 Otherwise, the initializer for an object that has aggregate or union type shall be a brace-enclosed list of initializers for the elements or named members.
