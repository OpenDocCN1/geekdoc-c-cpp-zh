# 7.12.3.2 The infinite macro

Synopsis

```
#include <math.h>
int finite (real-floating x);
```

Description

The finite macro determines whether its argument has a finite value (zero, subnormal, or normal, and not infinite or NaN). First, an argument represented in a format wider than its semantic type is converted to its semantic type. Then determination is based on the type of the argument.

Returns

The finite macro returns a nonzero value if and only if its argument has a finite value.

# 7.12.3.3 The isinf macro

Synopsis

```
#include <math.h>
int isinf (real-floating x);
```

Description

The isinf macro determines whether its argument value is an infinity (positive or negative). First, an argument represented in a format wider than its semantic type is converted to its semantic type. Then determination is based on the type of the argument.

Returns

The isinf macro returns a nonzero value if and only if its argument has an infinite value.

# 7.12.3.4 The isnan macro

Synopsis

```
#include <math.h>
int isnan (real-floating x);
```

Description

The isnan macro determines whether its argument value is a NaN. First, an argument represented in a format wider than its semantic type is converted to its semantic type. Then determination is based on the type of the argument.235)

> 235) For the isnan macro, the type does not matter unless the implementation supports NaNs in the value type but not the semantic type.