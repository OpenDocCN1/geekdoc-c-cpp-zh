# F10.7.2 The remainder functions

+   1 The **remainder** functions are fully specified as a basic arithmetic operation in
IEC 60559.

+   2 When subnormal results are supported, the returned value is exact and is independent of
the current rounding direction mode.

# F10.7.3 The remquo functions

+   1 The **remquo** functions follow the specifications for the *remainder* functions. They
have no further specifications special to IEC 60559 implementations.

+   2 When subnormal results are supported, the returned value is exact and is independent of
the current rounding direction mode.

# F10.8 Manipulation functions

# F10.8.1 The copysign functions

+   1 copys is specified in the Appendix to IEC 60559.

+   2 The returned value is exact and is independent of the current rounding direction mode.

# F10.8.2 The nan functions

+   1 All IEC 60559 implementations support quiet NaNs, in all floating formats.

+   2 The returned value is exact and is independent of the current rounding direction mode.

# F10.8.3 The nextafter functions

+   - **nextafter**(x, y) raises the “overflow” and “inexact” floating-point exceptions
for x and the function value infinite.

+   - **nextafter**(x, y) raises the “underflow” and “inexact” floating-point
exceptions for the value subnormal or zero and $x \neq y$.

+   2 Even though underflow or overflow can occur, the returned value is independent of
the current rounding direction mode.

# F10.8.4 The nexttoward functions

+   1 No additional requirements beyond on **nextafter**.

+   2 Even though underflow or overflow can occur, the returned value is independent of
the current rounding direction mode.