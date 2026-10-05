
s1, not compatible with the types struct s2, t2, the type pointed to is tp2, or int.

# EXAMPLE 3 The following obscure constructions

```c
typedef signed int t;
typedef int plain;
struct {
    unsigned t:4;
    const t:5;
    plain r:5;
};
```

declare a typedef name t with type signed int, a typedef name t contains values in the range [0, 15], an unnamed const-qualified bit-field (if it could be accessed) would contain values in the range [-15, +15] or [-16, +15], and named r t contains values in one of the ranges [0, 31], [-15, +15] (The choice of range is implementation-defined). The first two bit-field declarations differ in that unsigned is a type qualifier (forces t to be the name of a structure member), while const is a type qualifier (which modifies t is still visible as a typedef name). If these declarations are followed in an inner scope

```c
t f(t (t));
long t;
```

then a function f is declared with type "function returning signed int with one unnamed parameter with type pointer to returning signed int with one unnamed parameter with type signed int", and an identifier t with type long int.

# EXAMPLE 4 On the other hand, typedef names can be used to improve code readability. All three of the following declarations of the signal function specify exactly the same type, the first without making use of any typedef names.

```c
typedef void fv(int), (*pfv) (int);
void (*signal(int, void (*)) (int);
f *signal(int, f *);
pfv signal(int, pfv);
```

# EXAMPLE 5 If a typedef name denotes a variable length array type, the length of the array is fixed at the time typedef name is defined, not each time it is used:

```c
void copyopt(int n)
{
    typedef int B[n]; // B is n ints, n evaluated now
    n += 1;
    B a; // a is n ints, n without += 1
    int b[n]; // a and b are different sizes
    for (int i = 1; i < n; i++)
        a[i-1] = b[i];
}
```

## 6.7.9 Initialization

### Syntax

```c
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

### Constraints

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

then the current object (defined below) shall be structure or union type and the identifier shall be the name of a member of that type.

### Semantics

8 An initializer specifies the initial value stored in an object.

9 Except where explicitly stated otherwise, for the purposes of this subclause unnamed members of structure and union type do not participate in initialization. Unnamed members of structure objects have indeterminate value even after initialization.

10 If an object has automatic storage duration is not initialized explicitly, its value is not initialized explicitly. If an object has static or thread duration is not initialized explicitly, then:

- if it has pointer type, it is initialized to a null pointer;
- if it has arithmetic type, it is initialized to (positive or unsigned) zero;
- if it is an aggregate, every member is initialized (recursively) according to these rules, and any padding is initialized to zero bits;
- if it is a union, the first named member is initialized (recursively) according to these rules, and any padding is initialized to zero bits;

11 The initializer for a scalar shall be a single expression, optionally enclosed in braces. The initial value of the object is that of the expression (after conversion); the same type constraints and conversions as for simple assignment apply, taking the type of the scalar to be the qualified version of its declared type.

12 The rest of this subclause deals with initializers for objects that have aggregate or union type.

13 The initializer for a structure or union object that has automatic storage duration shall be either an initializer list as described below, or a single expression that has compatible structure or union type. In the latter case, the initial value of the object, including unnamed members, is that of the expression.

14 An array of character type may be initialized by a character string literal or UTF–8 string literal, optionally enclosed in braces. Successive bytes of the string literal (including the terminating null character if there is room or if the array is of unknown size) initialize the elements of the array.

15 An array with type compatible with char_t, char16_t, or char32_t may be initialized by a wide string literal with the corresponding prefix (L, u, or U), optionally enclosed in braces. Successive characters of the string literal (including the terminating null character if there is room or if the array is of unknown size) initialize the elements of the array.

16 Otherwise, the initializer for an object that has aggregate or union type shall be a brace-enclosed list of initializers.

Each brace-enclosed initializer list has an associated current object. When designations are present, the subjects of the current object are initialized in order according to the type of the current object: array elements in subscribing order, structure members in declaration order, and the first member of a union. In contrast, a designation causes the following initializer to begin initialization of the subobject described by the designator. Initialization then continues forward in order, beginning with the next subobject after that described by the designator.

Each designator begins its description with the current object associated with the closest brace pair. Each item in the designator list (in order) specifies a particular member of its current object and changes the current object for the next designator (if any) to be that. The current object that results at the end of the designator list is the subobject to be initialized by the following initializer.

The initialization shall occur in initializer list order, each initializer provided for a particular subobject overriding any previously listed initializer for the same subobject. All subjects that are not initialized shall be initialized implicitly the same as objects that have static storage duration.

If there are fewer initializers in a brace-enclosed list than there are elements or members of an aggregate, or fewer characters in a string literal used to initialize an array of size than there are elements in the array, the remainder of the aggregate shall be initialized implicitly the same as objects that have static storage duration.
