© ISO/IEC 2011 – All rights reserved
ISO/IEC 9899:2011 (E)

```
s1 = malloc(sizeof(struct s) + 10);
s2 = malloc(sizeof(struct s) + 6);
```

they behave as if the declarations were:

```
struct { int n; double d[1]; } *s1, *s2;
```

and:

```
double dp;
dp = &(s1->d[0]); // valid
*dp = 42; // valid
dp = &(s2->d[0]); // valid
*dp = 42; // undefined behavior
```

+   25 The assignment:
*s1 = *s2;

only copies the member n; if any of the array elements within the first sizeof(struct s) bytes of the structure, they may be copied or partially overwritten with indeterminate values.

+   26 EXAMPLE 3 Because members of anonymous structures and unions are considered to be members of the containing structure or union, struct s in the example has more than one named member and the use of a flexible array member is valid:

```
struct s {
    struct { int i; };n    int a[];
};
```

Forward references: declarators (6.7.6), tags (6.7.2.3).

# 6.7.2 Enumeration specifiers

Syntax

+   1 enum-specifier:
    enum identifier_opt { enumerator-list }
    enum identifier_opt { enumerator-list , }
    enum enumerator-list:
        enumerator
        enumerator-list , enumerator
enumerator:
    enumeration-constant
    enumeration-constant = constant-expression

# Constraints

+   2 The expression that defines the value of an enumeration constant shall be an integer constant expression that has a value representable as an int.

§6.7.2.2 Language 117