# G.6.3 Exponential and logarithmic functions

# G.6.3.1 The cexp functions

+   - cexp(conj(z)) = conj(cexp(z)).
- cexp(±0 +i0) returns 1 + i0.
- cexp(x +∞) returns NaN+iNaN and raises the “invalid” floating-point exception, for finite x.
- cexp(x +iNaN) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for finite x.
- cexp(+∞ +i0) returns ∞ +i0.
- cexp(-∞ + iy) returns +0 cis(y), for finite y.
- cexp(+∞ + iy) returns -∞ cis(y), for finite y.
- cexp(-∞ +∞) returns ±0±i0 (where the signs of the real and imaginary parts of the result are unspecified).
- cexp(+∞ +∞) returns ±∞+iNaN and raises the “invalid” floating-point exception (where the sign of the real part of the result is unspecified).
- cexp(-∞ +iNaN) returns ±0±i0 (where the signs of the real and imaginary parts of the result are unspecified).
- cexp(+∞ +iNaN) returns ∞+iNaN (where the sign of the real part of the result is unspecified).
- cexp(NaN +i0) returns NaN + i0.
- cexp(NaN + iy) returns NaN +iNaN and optionally raises the “invalid” floating-point exception, for all nonzero numbers y.
- cexp(NaN +iNaN) returns NaN +iNaN.

# G.6.3.2 The clog functions

+   - clog(conj(z)) = conj(clog(z)).
- clog(-0 +i0) returns -∞+iπ and raises the “divide-by-zero” floating-point exception.
- clog(+0 +i0) returns -∞ +i0 and raises the “divide-by-zero” floating-point exception.
- clog(x +∞) returns +∞π/2, for finite x.
- clog(x +iNaN) returns NaN +iNaN and optionally raises the “invalid” floating-point exception, for finite x.