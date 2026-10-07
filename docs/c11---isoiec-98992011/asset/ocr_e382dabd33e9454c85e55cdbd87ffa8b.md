# ISO/IEC 9899:2011 (E)

# © ISO/IEC 2011 – All rights reserved

+   - clog $(-\infty + iy)$ returns $+\infty + i\pi$, for finite positive-signed y.
- clog $(+\infty + iy)$ returns $+\infty + i0$, for finite positive-signed y.
- clog $(-\infty + io)$ returns $+\infty + i3\pi/4$.
- clog $(+\infty + io)$ returns $+\infty + i\pi/4.
- clog $(+\infty + iNaN)$ returns $+\infty + iNaN.
- clog $(NaN + iy)$ returns $NaN + iNaN$ and optionally raises the “invalid” floating-point exception, for finite y.
- clog $(NaN + +\infty)$ returns $+\infty + iNaN.
- clog $(NaN + iNaN)$ returns $NaN + iNaN.

# G.6.4 Power and absolute-value functions

# G.6.4.1 The cpow functions

The cpow functions raise floating-point exceptions if appropriate for the calculation of the parts of the result, and also may raise spurious floating-point exceptions.³379)

# G.6.4.2 The csqrt functions

+   csqrt $(conj(z)) = conj(csqrt(z))$.
- csqrt $(\pm0 + io)$ returns $+\infty + i0.
- csqrt $(x + i\infty)$ returns $+\infty + oo$, for all x (including NaN).
- csqrt $(x + iNaN)$ returns $NaN + iNaN$ and optionally raises the “invalid” floating-point exception, for finite x.
- csqrt $(-\infty + iy)$ returns $+\infty + i0$, for finite positive-signed y.
- csqrt $(+\infty + iy)$ returns $+\infty + i0$, for finite positive-signed y.
- csqrt $(-\infty + iNaN)$ returns $NaN \pm oo$ (where the sign of the imaginary part of the result is unspecified).
- csqrt $(+\infty + iNaN)$ returns $+\infty + iNaN.
- csqrt $(NaN + iy)$ returns $NaN + iNaN$ and optionally raises the “invalid” floating-point exception, for finite y.
- csqrt $(NaN + iNaN)$ returns $NaN + iNaN.

> 379) This allows cpow(z, c) to be implemented as cexp(c log(z)) with precluding implementations that treat special cases mayfully.

544

IEC 60559-compatible complex arithmetic

§G.6.4.2