© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

the preceding loop be treated as

```
if (0 < n) x = x + 1;
```

# F.9.2 Expression transformations

+   x/2 ↔ x × 0.5 Although similar transformations involving inexact constants generally do not yield numerically equivalent expressions, if the constants are exact such transformations can be made on IEC 60559 machines and others that round perfectly.

+   1 x and x/1 → x The expressions 1 x, and x/1 are equivalent (on IEC 60559 machines, among others).³368

+   x/x ↔ 1.0 The expressions x/x and 1.0 are not equivalent if x be zero, infinite, or Nan.

+   x - y ↔ x + (-y) The expressions x - y, x + (-y), and (-y) + x are equivalent (on IEC 60559 machines, among others).

+   x -y ↔ -(y) The expressions x - y and (-y) x are not equivalent because 1 − 1 is +0 (-1 in 1) is -0 (in the default rounding direction).³369

+   x - x ↔ 0.0 The expressions x - x and 0.0 are not equivalent if x be a NaN or infinite.

+   0 × x ↔ 0.0 The expressions 0 x and 0.0 are not equivalent if x is a NaN, infinite, or -0.

+   x + 0 → x The expressions x + 0 and x are not equivalent if x be -0, because (-0) + (+0) yields +0 (in the default rounding direction), not -0.

+   x - 0 → x (+0)- (+0) yields -0 when rounding is towards (∞), or otherwise, and (-0)-(+0) always yields -0; so, if the state of the FENV_ACCESS pragma is “off”, default rounding, then the implementation can replace x −0 by x, even if x might be zero.

+   -x ↔ 0 - x The expressions -x and 0 - x are not equivalent if x is +0, because (+0) yields -0, but 0-(0) yields +0 (unless rounding is downward).

> 368 Strict support for signaling NaNs — not required by this specification — would invalidate these and other transformations that require arithmetic operations.

> 369 IEC 60559 prescribes a sign zero to preserve mathematical identities across certain discontinuities. Examples include:

1/(1 ±0) is ±0
and conj(sqrt(z)) is sqrt(conj(z)), for complex z.

§9.2 IEC 60559 floating-point arithmetic 515

Copyright International Organization for Standardization
Provided by IHS under license with ISO
No reproduction or networking permitted without license from IHS
Not for Resale