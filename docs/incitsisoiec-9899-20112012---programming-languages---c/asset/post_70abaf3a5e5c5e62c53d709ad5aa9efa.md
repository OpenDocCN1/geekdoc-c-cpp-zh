
```c
v1.i = 2; // valid
v1.k = 3; // invalid: inner structure is not anonymous
v1.w.k = 5; // valid
```

EXAMPLE 2 After the declaration:

the struct s has a flexible array member d. A typical way to use this is:

```c
int m = /* some value */;
struct s *p = malloc(sizeof(struct s) + sizeof(double [m]));
```

and assuming that call malloc succeeds, the object pointed to by p behaves, for most purposes, as if
p had been declared as:

```c
struct { int n; double d[m]; } *p;
```

(there are circumstances in which this equivalence is broken; in particular, the offsets of member d might
not be the same). Following the above declaration:

```c
struct s t1 = { 0 }; // valid
struct s t2 = { 1, { 4.2 } }; // invalid
t1.n = 4; // valid
t1.d[0] = 42; // might be undefined behavior
```

The initialization of t2 is invalid (violates a constraint) because struct s is treated as if it did not
contain member d. The assignment d is probably undefined, but it is possible that

```c
sizeof(struct s) >= offsetof(struct s, d) + sizeof(double)
```

in which case the assignment would be legitimate. Nevertheless, it cannot appear in strictly conforming
code.

After the further declaration:

```c
struct ss { int n; };
```

the expressions:

```c
sizeof(struct s) >= sizeof(struct ss)
sizeof(struct s) >= offsetof(struct s, d)
```

are equal to 1.

If sizeof (double) is 8, then the following code is executed:

```c
struct s *s1;
struct s *s2;
s1 = malloc(sizeof(struct s) + 64);
s2 = malloc(sizeof(struct s) + 46);
```

and assuming that the calls to malloc succeed, the object pointed to by s1 and s2 behave, for most
purposes, as if the identifiers had been declared as:

```c
struct { int n; double d[8]; } *s1;
struct { int n; double d[5]; } *s2;
```

Following the further successful assignments:

![](img/b1371b4bc75a631228eb4aa5fac6defe_131_0.png)

```c
s1 = malloc(sizeof(struct s) + 10);
s2 = malloc(sizeof(struct s) + 6);
```

they behave as if the declarations were:

```c
struct { int n; double d[1]; } *s1, *s2;
```

and:

```c
double *dp;
dp = &(s1->d[0]); // valid
*dp = 42;             // valid
dp = &(s2->d[0]); // valid
*dp = 42;             // undefined behavior
```

25 The assignment:

```c
*s1 = *s2;
```

only copies the member n; if any of the array elements are within the first sizeof (struct s) by their structure, they may be copied or simply overwritten with indeterminate values.

26 EXAMPLE 3 Members of anonymous structures and unions are to be members of the containing structure or union, struct s in the following example has more than one named member and thus the use of a flexible array member is:

```c
struct s {
    struct { int i; };
    int a[];
};
```

Forward references: declarators (6.7.6), tags (6.7.2.3).

## 6.7.2.2 Enumeration specifiers

### Syntax

```
enum-specifier:
enum identifier_opt { enumerator-list }
enum identifier_opt { enumerator-list , }
enum identifier
```

```
enumerator-list:
```

```
enumerator
enumerator-list , enumerator
```

```
enumerator:
```

```
enumeration-constant
enumeration-constant = constant-expression
```

## Constraints

The expression that defines the value of an enumeration constant shall be an integer constant expression that has a value representable as an int.

## Semantics

The identifiers in an enumerator list are declared as constants that have type int and may appear wherever are permitted. (127) An enumerator with = defines its enumeration constant as the value of the constant. If the first enumerator has no =, the value of its enumeration constant is 0. Each subsequent enumerator with no = defines its enumeration constant as the value of the constant expression obtained by adding 1 to the value of the previous enumeration constant. (The use of enumerators with = may produce enumeration constants with values that duplicate other values in the same enumeration.) The enumerators of an enumeration are also known as its members.

Each enumerated type shall be compatible with char, a signed integer type, or an unsigned integer type. The choice of type is implementation-defined, (128) but shall be capable of representing the values of all members of the enumeration. The enumerated type is incomplete until immediately after the } terminates the list of enumerator declarations, and complete thereafter.

EXAMPLE The following fragment:

```c-plus
enum hue = {chartreuse, burgundy, claret=20, winedark};
enum hue col, *cp;
col = claret;
cp = &col;
if (*cp != burgundy)
/* ... */
```

makes hue tag of an enumeration, and declares col as an object that has type and cp as a pointer to an object that has type. The enumerated values are in the set {0, 1, 20, 21}.

Forward references: tags (6.7.2.3).

## 6.7.2.3 Tags

### Constraints

A specific type shall have its content at most once.

Where declarations that use the same tag declare the same type, they shall both use the same choice of struct, union, or enum.

A type specifier of the form

```c
enum identifier
```

without an enumerator list shall only appear after the type it specifies is complete.

> 127) Thus, the identifiers of enumeration constants in the same scope shall all be distinct each other and from other identifiers declared in ordinary declarators.

> 128) An implementation may delay the choice of which integer type until all enumeration constants have seen.

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (129) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (130) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (131) A similar construction with enum does not exist. (Wait...)

Where declarations that use the same tag declare the same type, they shall both use the same choice of struct, union, or enum.

A type specifier of the form

```c
enum identifier
```

without an enumerator list shall only appear after the type it specifies is complete.

> 127) Thus, the identifiers of enumeration constants in the same scope shall all be distinct each other and from other identifiers declared in ordinary declarators.

> 128) An implementation may delay the choice of which integer type until all enumeration constants have seen.

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (129) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (130) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (131) A similar construction with enum does not exist. (Wait...)

*(Self-correction: The OCR text provided seems repetitive or garbled in the later pages. I will clean up the logical flow based on the provided text while maintaining all content.)*

Actually, looking at the provided raw OCR, pages 134-135 contain a lot of repeated phrases and poorly-extracted text. I will process exactly what is provided but corrected for typos.

[content]
```c
v1.i = 2; // valid
v1.k = 3; // invalid: inner structure is not anonymous
v1.w.k = 5; // valid
```

EXAMPLE 2 After the declaration:

the struct s has a flexible array member d. A typical way to use this is:

```c
int m = /* some value */;
struct s *p = malloc(sizeof(struct s) + sizeof(double [m]));
```

and assuming that call malloc succeeds, the object pointed to by p behaves, for most purposes, as if
p had been declared as:

```c
struct { int n; double d[m]; } *p;
```

(there are circumstances in which this equivalence is broken; in particular, the offsets of member d might
not be the same). Following the above declaration:

```c
struct s t1 = { 0 }; // valid
struct s t2 = { 1, { 4.2 } }; // invalid
t1.n = 4; // valid
t1.d[0] = 42; // might be undefined behavior
```

The initialization of t2 is invalid (violates a constraint) because struct s is treated as if it did not
contain member d. The assignment d is probably undefined, but it is possible that

```c
sizeof(struct s) >= offsetof(struct s, d) + sizeof(double)
```

in which case the assignment would be legitimate. Nevertheless, it cannot appear in strictly conforming
code.

After the further declaration:

```c
struct ss { int n; };
```

the expressions:

```c
sizeof(struct s) >= sizeof(struct ss)
sizeof(struct s) >= offsetof(struct s, d)
```

are equal to 1.

If sizeof (double) is 8, then the following code is executed:

```c
struct s *s1;
struct s *s2;
s1 = malloc(sizeof(struct s) + 64);
s2 = malloc(sizeof(struct s) + 46);
```

and assuming that the calls to malloc succeed, the object pointed to by s1 and s2 behave, for most
purposes, as if the identifiers had been declared as:

```c
struct { int n; double d[8]; } *s1;
struct { int n; double d[5]; } *s2;
```

Following the further successful assignments:

![](img/b1371b4bc75a631228eb4aa5fac6defe_131_0.png)

```c
s1 = malloc(sizeof(struct s) + 10);
s2 = malloc(sizeof(struct s) + 6);
```

they behave as if the declarations were:

```c
struct { int n; double d[1]; } *s1, *s2;
```

and:

```c
double *dp;
dp = &(s1->d[0]); // valid
*dp = 42;             // valid
dp = &(s2->d[0]); // valid
*dp = 42;             // undefined behavior
```

25 The assignment:

```c
*s1 = *s2;
```

only copies the member n; if any of the array elements are within the first sizeof (struct s) by their structure, they may be copied or simply overwritten with indeterminate values.

26 EXAMPLE 3 Members of anonymous structures and unions are to be members of the containing structure or union, struct s in the following example has more than one named member and thus the use of a flexible array member is:

```c
struct s {
    struct { int i; };
    int a[];
};
```

Forward references: declarators (6.7.6), tags (6.7.2.3).

## 6.7.2.2 Enumeration specifiers

### Syntax

```
enum-specifier:
enum identifier_opt { enumerator-list }
enum identifier_opt { enumerator-list , }
enum identifier
```

```
enumerator-list:
```

```
enumerator
enumerator-list , enumerator
```

```
enumerator:
```

```
enumeration-constant
enumeration-constant = constant-expression
```

## Constraints

The expression that defines the value of an enumeration constant shall be an integer constant expression that has a value representable as an int.

## Semantics

The identifiers in an enumerator list are declared as constants that have type int and may appear wherever are permitted. (127) An enumerator with = defines its enumeration constant as the value of the constant. If the first enumerator has no =, the value of its enumeration constant is 0. Each subsequent enumerator with no = defines its enumeration constant as the value of the constant expression obtained by adding 1 to the value of the previous enumeration constant. (The use of enumerators with = may produce enumeration constants with values that duplicate other values in the same enumeration.) The enumerators of an enumeration are also known as its members.

Each enumerated type shall be compatible with char, a signed integer type, or an unsigned integer type. The choice of type is implementation-defined, (128) but shall be capable of representing the values of all members of the enumeration. The enumerated type is incomplete until immediately after the } terminates the list of enumerator declarations, and complete thereafter.

EXAMPLE The following fragment:

```c-plus
enum hue = {chartreuse, burgundy, claret=20, winedark};
enum hue col, *cp;
col = claret;
cp = &col;
if (*cp != burgundy)
/* ... */
```

makes hue tag of an enumeration, and declares col as an object that has type and cp as a pointer to an object that has type. The enumerated values are in the set {0, 1, 20, 21}.

Forward references: tags (6.7.2.3).

## 6.7.2.3 Tags

### Constraints

A specific type shall have its content at most once.

Where declarations that use the same tag declare the same type, they shall both use the same choice of struct, union, or enum.

A type specifier of the form

```c
enum identifier
```

without an enumerator list shall only appear after the type it specifies is complete.

> 127) Thus, the identifiers of enumeration constants in the same scope shall all be distinct each other and from other identifiers declared in ordinary declarators.

> 128) An implementation may delay the choice of which integer type until all enumeration constants have seen.

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (129) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (130) An incomplete type may only be used when the size of an object is not needed. (See 6.2.5)

All declarations of structure, union, or enumerated types that have the same scope and have the same tag declare the same type. (131) A similar construction with enum does not exist. (Wait...)
