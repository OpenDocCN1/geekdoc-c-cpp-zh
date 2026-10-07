# 7.12.2 The FP_CONTRACT pragma

Synopsis

```
#include <math.h>
#pragma STDC FP_CONTRACT on-off-switch
```

Description

The FP_CONTRACT pragma can be used to allow (if the state is "on") or disallow (if the state is "off") the implementation to contract expressions (6.5). Each pragma can occur either outside external declarations or preceding all explicit declarations and statements inside a compound statement. When outside external declarations, the pragma takes effect from its occurrence until another FP_CONTRACT pragma is encountered, or until the end of the translation unit. When inside a compound statement, the pragma takes effect from its occurrence until another FP_CONTRACT pragma is encountered (within a nested compound statement), or until the end of the compound statement; at the end of a compound statement the state for the pragma is restored to its condition before the compound statement. If the pragma is used in any other context, the behavior is undefined. The default state ("on" or "off") for the pragma is implementation-defined.

# 7.12.3 Classification macros

In the synopses in this subclause, real-floating indicates that the argument shall be an expression of real-floating type.

# 7.12.3.1 The fpclassify macro

Synopsis

```
#include <math.h>
int fpclassify(real-floating x);
```

Description

The fpclassify macro classifies its argument value as NaN, infinite, normal, subnormal, zero, or into another implementation-defined category. First, an argument represented in a format wider than its semantic type is converted to its semantic type. Then classification is based on the type of the argument.

Returns

The fpclassify macro returns the value of the number classification macro appropriate to the value of its argument.

> 234) Since an expression can be evaluated with more range and precision than its type, it is important to know the type that classification is based on. For example, a long double value might become subnormal when converted to double, and zero when converted to float.