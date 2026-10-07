# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

```
v1.i = 2;           // valid
v1.k = 3;           // invalid: inner structure is not anonymous
v1.w.k = 5;         // valid
```

20 EXAMPLE 2 After the declaration:

```
struct s { int; double d[]; };

struct s has a flexible array d. A typical way to use this is:

int m = /* some value */;
struct s *p = malloc(sizeof(struct s) + sizeof(double [m]));
```

and assuming that the call to malloc succeeds, the object pointed to by p behaves, for most purposes, as if p had been declared as:

```
struct { int n; double d[m]; } *p;

(there are circumstances in which this equivalence is broken; in particular, the offsets of member might not be the same).
```

21 Following the declaration:

```
struct s t1 = { };       // valid
struct s t2 = { 1, 4.2 }; }; // invalid
t1.n = 4;                // valid
t1.d[0] = 4.2;          // might be undefined behavior
```

The initialization of t2 is invalid (and violates a constraint) because struct s is treated as if it did not contain member d. The assignment to t1.d[0] is probably undefined behavior, but it is possible

```
sizeof(struct s) >= offsetof(struct s, d) + sizeof(double)
```

in which case the assignment would be meaningless. However, it cannot appear in strictly conforming code.

22 After the declaration:

```
struct s { int n; };
```

the expressions:

```
sizeof(struct s) >= sizeof(struct s)
sizeof(struct s) >= offsetof(struct s, d)
```

are always equal to 1.

23 If sizeof(double) is 8, then after the following code is executed:

```
struct s *s1;
struct s *s2;
s1 = malloc(sizeof(struct s) + 64);
s2 = malloc(sizeof(struct s) + 46);
```

and assuming that the call to malloc succeeds, the objects pointed to by s1 and s2 behaves, for most
poses, as if the identifiers had been declared as:

```
struct { int n; double d[8]; } *s1;
struct { int n; double d[5]; } *s2;
```

24 Following this successful assignments: