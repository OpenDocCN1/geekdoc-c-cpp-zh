# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

22 If an array of unknown size is initialized, its size is determined by the largest indexed element with an explicit initializer. The array type is completed at the end of its initializer list.

23 The evaluations of the initialization list expressions are indeterminately sequenced with respect to one another and the order in which any side effects occurs is unspecified.152

24 EXAMPLE 1 Provided that \<complex.h\gt> has been #included, the declarations

```
int i = 3.5;
double complex c = 5 + 3 * I;
```

define and initialize i with the value 3 and c with the value 5.0 +i3.0.

25 EXAMPLE 2 The declaration

```
int x[] = { 1, 3, 5 };
```

defines and initializes x as a one-dimensional array object that has three elements, as no size was specified and there are three initializers.

26 EXAMPLE 3 The declaration

```
int y[4] = {
{ 1, 3, 5 },
{ 2, 4, 6 },
{ 3, 5, 7 };
;
```

is a definition with a fully bracketed initialization: 1, 3, and 5 initialize the first row of y (the array y[0]), namely y[0][0], y[0][1], and y[0][2]. Likewise the next two lines initialize y[1] and y[2]. The initializer ends early, so y[3] is initialized with zeros. Precisely the same effect could have achieved by

```
int y[4][3] = {
{ 1, 3, 5, 2, 4, 6, 3, 5, 7 }
;
```

The initializer for y[0] does not begin with a left brace, so three from the list are used. Likewise the next three are taken successively for y[1] and y[2].

27 EXAMPLE 4 The declaration

```
int z[4][3] = {
{ 1 }, { 2 }, { 3 }, { 4 }
;
```

initializes the first column of z as specified and the rest with zeros.

28 EXAMPLE 5 The declaration

```
struct { int a[3]; } w[] = { 1 }, { 2 };
```

is a definition with an inconsistently bracketed initialization. It defines an array with two element

152) In particular, the evaluation order is not the same as the order of subobject initialization.

142

Language

§6.7.9