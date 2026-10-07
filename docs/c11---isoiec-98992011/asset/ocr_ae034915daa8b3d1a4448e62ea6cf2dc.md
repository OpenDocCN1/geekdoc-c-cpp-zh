© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

Forward references: IEC 60559-compatible complex arithmetic (annex G).

# 7.3.2 Conventions

+   Values are interpreted as radians, not degrees. An implementation may set errno but is not required to.

# 7.3.3 Branch cuts

+   Some of the functions below have branch cuts, across which the function is discontinuous. For implementations that follow a signed zero (including all IEC 60559 implementations) follow the specifications of annex G, the sign of zero distinguishes one side of a cut from another the function is continuous (except for format limitations) as the cut is approached from either side. For example, the square root function, which has a branch cut along the negative real axis, the top of the cut, with imaginary part +0, maps to the positive imaginary axis, and the bottom of the cut, with imaginary part -0, maps to the negative imaginary axis.

+   Implementations that do not support a signed zero (see annex F) cannot distinguish the sides of branch cuts. These implementations map a cut so the function is continuous as the cut is approached around the endpoint of the cut in a counter clockwise direction. (Branch cuts for the functions specified here have just one endpoint.) For example, for the square root function, going counter clockwise around the finite endpoint of the cut along the negative real axis approaches the cut from above, so the cut maps to the positive imaginary axis.

# 7.3.4 The CX_LIMITED_RANGE pragma

Synopsis

```
#include <complex.h>
#pragma STDC CX_LIMITED_RANGE on-switch
```

Description

+   The usual mathematical formulas for complex multiply, divide, and absolute value are problematic because of their treatment of infinities and because of underflow and overflow. The CX_LIMITED_RANGE pragma can be used to inform the implementation (where the state is "on") the usual mathematical formulas are acceptable.¹195} The pragma can occur either external declarations or preceding all explicit declarations and statements inside a compound statement. When external declarations, the pragma takes effect from its occurrence until another CX_LIMITED_RANGE pragma is encountered, or until the end of the translation unit. When inside a compound statement, the pragma takes effect from its occurrence until another CX_LIMITED_RANGE pragma is encountered (including within a nested compound statement), or until the end of the compound statement; at the end of a compound statement for the state is restored to its condition just before

$7.3.4 Library 189