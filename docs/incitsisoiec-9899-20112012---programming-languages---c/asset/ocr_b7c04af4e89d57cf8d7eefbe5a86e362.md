shown. Unless otherwise specified, the symbol “±” occurs in an argument and the result, the result has the same sign as the argument.

The functions are continuous on both sides of their branch cuts, taking into account the sign of zero. For example, csqrt (-2±i0) = ±i√2.

Since complex and imaginary values are computed of real values, each function may be regarded as computing real values from real values. Except as noted, the functions treat real infinities, NaNs, signed zeros, subnormals, and the floating-exception flags in a manner consistent with the specifications for real values in F.10,378

The functions cag, conj, cproj, and creal are fully specified for all implementations, including IEC 60559, in 7.3.9. These functions raise floating-point exceptions.

Each of the functions cabs and carg is specified by a formula in terms of a real function (whose special cases are covered in annex F

```
cabs (x + iy) = hypot(x, y)
carg (x + iy) = atan2(y, x)
```

Each of the functions casin, catan, cccos, csin, and ctan is specified implicitly by a formula in terms of other complex functions (whose special cases are specified below):

```
casin(z) = -i casin(iz)
catan(z) = -i catanh(iz)
ccos(z) = -i ccosh(iz)
sin(z) = -i csinh(iz)
an(z) = -i tanh(iz)
```

For the other functions, the following subclauses specify behavior for special cases, including treatment of the “invalid” and “divide-by-zero” floating-point exceptions. For families of functions, the specifications apply to all of the functions. For a function f satisfying f(conj(z))=conj(f(z)), the specifications for the upper half-plane imply the specifications for the lower half-plane; if the function f is either even, f(-z)=f(z), or odd, f(-z)=-f(z), then the specifications for the first quadrant imply the specifications for the other three quadrants.

In the following subclauses, cis(y) is defined as cos(y)+i sin(y).

378) As noted in G.3, a complex value with at least one infinite part is regarded as an infinity even if its other part is a NaN.