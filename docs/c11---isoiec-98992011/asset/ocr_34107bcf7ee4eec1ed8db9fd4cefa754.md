# G.6.3 Exponential and logarithmic functions

# G.6.3.1 The cexp functions

+   - cexp(conj(z)) = conj(cexp(z)).
- cexp(±0+i0) returns 1+i0.
- cexp(x + ioo) returns NaN+iNaN and raises the “invalid” floating-point exception, for finite x.
- cexp(x +iNaN) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for finite x.
- cexp(±oo +i0) returns +oo+i0.
- cexp(-oo + iy) returns +0 cis(y), for finite y.
- cexp(+oo + iy) returns +oo cis(y), for nonzero y.
- cexp(±oo + ioo) returns ±oo±oo (where the signs of the real and imaginary parts of the result are unspecified).
- cexp(+oo +∞) returns ±oo+∞ and raises the “invalid” floating-point exception (where the sign of the real part of the result is unspecified).
- cexp(-oo +iNaN) returns ±0±i0 (where the signs of the real and imaginary parts of the result are unspecified).
- cexp(+oo +iNaN) returns ±oo+iNaN (where the sign of the real part of the result is unspecified).
- cexp(NaN +i0) returns NaN+i0.
- cexp(NaN + iy) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for all nonzero y.
- cexp(NaN +iNaN) returns NaN+iNaN.

# G.6.3.2 The clog functions

+   - clog(conj(z)) = conj(clog(z)).
- clog(±0+i0) returns -oo+ix and raises the “divide-by-zero” exception.
- clog(+0+i0) returns -oo+i0 and raises the “divide-by-zero” exception.
- clog(x + ioo) returns +oo+iπ2, for finite x.
- clog(x + iNaN) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for finite x.