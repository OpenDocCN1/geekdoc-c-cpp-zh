+   - cacosh(NaN+iy) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for finite y.

+   - cacosh(NaN+ico) returns ∞+iNaN.

+   - cacosh(NaN+iNaN) returns NaN+iNaN.

# G.6.2.2 The casinh functions

+   - casinh(conj(z)) = conj(casinh(z)) and casinh is odd.

+   - casinh(+0+i0) returns 0+i0.

+   - casinh(x+∞) returns ∞+π/2 for positive-signed finite x.

+   - casinh(x+iNaN) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for finite x.

+   - casinh(∞+iy) returns ∞+i0 for positive-signed finite y.

+   - casinh(∞+i0) returns ∞+π/4.

+   - casinh(∞+iNaN) returns ∞+iNaN.

+   - casanh(NaN+i0) returns NaN+i0.

+   - casanh(NaN+iy) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for nonzero y.

+   - casanh(NaN+∞) returns ±+iNaN (when the sign of the real part of the result is unspecified).

+   - casanh(NaN+iNaN) returns NaN+iNaN.

# G.6.2.3 The catanh functions

+   - catanh(conj(z)) = conj(catanh(z)) and catanh is odd.

+   - catanh(+0+i0) returns 0+i0.

+   - catanh(+0+iNaN) returns 0+iNaN.

+   - catanh(+1+i0) returns ∞+i0 and raises the “divide-by-zero” floating-point exception.

+   - catanh(x+∞) returns ∞+π/2, for finite positive-signed x.

+   - catanh(x+iNaN) returns NaN+iNaN and optionally raises the “invalid” floating-point exception, for nonzero finite x.

+   - catanh(∞+iy) returns +0+π/2, for finite positive-signed y.

+   - catanh(∞+∞) returns +0+π/2.

+   - catanh(∞+iNaN) returns +0+iNaN.