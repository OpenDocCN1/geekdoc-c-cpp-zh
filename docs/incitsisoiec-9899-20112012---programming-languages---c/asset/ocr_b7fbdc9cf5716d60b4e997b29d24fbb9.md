if the first operand is a nonzero number or an infinity and the second operand is a zero, the result of the / operator is an infinity.

If both operands of the * operator are complex or if the second operand of the / operator is complex, the operator represents floating-point exceptions if appropriate for the calculation of the parts, and may result in spurious floating-point exceptions.

EXAMPLE Multiplication of doubleComplex could be implemented as follows. Note that the imaginary unit I has imaginary type (see G.6).

```
#include <math.h>
#include <complex.h>
/* Multiply z * w ... */
double complex * Cmultdt(double z, double w)
{
    #pragma STDC FP_CONTRACT OFF
double a, b, c, d, ad, bd, bc, x, y;
    a = real(z); b = imag(z);
    c = real(w); d = imag(w);
    ac = a * c; bd = b * d;
    ad = a * d; bc = b * c;
    x = ac - bd; y = ad + bc;
    if (/* Recover infinities that computed as NaN+iNaN ... */
        int recalc = 0;
        if (isinf(a) || isinf(b)) { // z is infinite
            /* "Box" the infinity and change NaNs in the other factor to 0 */
            a = copysign(isinf(a) ? 1.0 : 0.0, a);
            b = copysign(isinf(b) ? 1.0 : 0.0, b);
            if (isinf(c)) c = copysign(0.0, c);
            if (isinf(d)) d = copysign(0.0, d);
            recalc = 1;
        }
        if (isinf(c) || isinf(d)) { // w is infinite
            /* "Box" the infinity and change NaNs in the other factor to 0 */
            c = copysign(isinf(c) ? 1.0 : 0.0, c);
            d = copysign(isinf(d) ? 1.0 : 0.0, d);
            if (isinf(a)) a = copysign(0.0, a);
            if (isinf(b)) b = copysign(0.0, b);
            recalc = 1;
        }
        if (!recalc && (isinf(ac) || isinf(bd) ||
            isinf(ad) || isinf(bc))) {
            /* Recover infinities from overflow by changing NaNs to 0... */
            if (isinf(a)) a = copysign(0.0, a);
            if (isinf(b)) b = copysign(0.0, b);
            if (isinf(c)) c = copysign(0.0, c);
            if (isinf(d)) d = copysign(0.0, d);
            recalc = 1;
        }
    if (recalc) {
```