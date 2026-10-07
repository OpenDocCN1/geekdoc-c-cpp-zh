# ISO/IEC 9899:2011 (E)
ISO/IEC 2011 – All rights reserved

If two elements compare as equal, their order in the resulting sorted array is unspecified.

Returns

The qsort function returns no value.

# 7.22.6 Integer arithmetic functions

# 7.22.6.1 The abs, labs and lldabs functions

Synopsis

```
#include <stdlib.h>
int abs(int j);
long int labs(long int j);
long long lldabs(long long int j);
```

Description

The abs, labs, and lldabs functions compute the absolute value of an integer j. If the result cannot be represented, the behavior is undefined.304

Returns

The abs, labs, and lldabs functions return the absolute value.

# 7.22.6.2 The div, lldiv, and l11div functions

Synopsis

```
#include <stdlib.h>
div_t div(int numer, int denom);
lldiv_t lldiv(long int numer, long int denom);
l11div_t l11div(long long numer, long long int denom);
```

Description

The div, lldiv, and l11div, functions compute numer / denom % denom in a single operation.

Returns

The div, lldiv, and l11div functions return a structure of type div_t, ldiv_t, and l11div_t, respectively, comprising both the quotient and the remainder. The structures shall contain (in either order) the members quot (the quotient) and rem (the remainder), each of which has the same as the arguments numer and denom. If either part of the result cannot be represented, the behavior is undefined.

> 304 The absolute value of the negative number cannot be represented in two's complement.

356
Library
7.22.6.2