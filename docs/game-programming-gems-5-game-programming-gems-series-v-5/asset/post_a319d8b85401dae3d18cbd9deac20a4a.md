
float sinB = .999999953f*( -.999990537f*( .4166365617e-1f
+ ( -.138537094e-2f+ .2315401401e-4f*B)*B)*B;
float alpha = sinA * mRecipSqrt;
float beta = sinB * mRecipSqrt;
return Quat( alpha * mA.X + beta * mB.X, alpha * mA.Y + beta * mB.Y,
alpha * mA.Z + beta * mB.Z, alpha * mA.W + beta *
mB.W );
}
private:
float mTheta;
float mRecipSqrt;
const Quat &mA;
const Quat &mB;
};

This class shows the result we obtain when we simply approximate the component functions of the traditional slerp function.

## Matrix Approximation

Because \(\beta(x,t)\) is simply a function of two variables, we can, in theory, represent the entire result as a two-dimensional polynomial in \(x\) and \(t\). That is,

\(\beta(x,t) = \mathbf{XMT}\) (2.4.23)

where \(\mathbf{M}\) is an \(N_x \times N_t\) matrix and

\(\mathbf{X} = (1 \quad x \quad \dots \quad x^{N_x-1})\)
\(\mathbf{T} = (t \quad t^2 \quad \dots \quad t^{N_t-1}).\) (2.4.24)

Applying the same process as in the analysis of \(\arccos(x)\), namely using the Maple series command, we see that we have a problem approximating the whole polynomial because

\(\lim_{x \to 1} \beta(x,t) = \infty.\) (2.4.25)

We need to take this singularity out of the function so that we can approximate it with fewer terms.

If we evaluate

\(g(x,t) = \beta(x,t)(1+x)\) (2.4.26)

instead, then we end up with a much better behaved function over the range \(x \in [-1, 1]\), as illustrated in Figure 2.4.10. We can then multiply by \(1/(1+x)\) to obtain \(\beta(x,t)\).

![](img/672fe9a2d008ba627b1991e15d70f43e_301_0.png)

FIGURE 2.4.10 g(x,t), a better alternative to approximating β(x,t).

Unfortunately, Maple does not come with a 2D version of the minimax command, and besides, uniform error distribution is useful only in certain conditions.

We can make a 2D version of the Chebyshev approximation method, which constructs a function in the form

```
\(\sum_{j=0}^N \sum_{i=0}^N c_{i,j} T(i,x)T(j,t)\) (2.4.27)
```

where T(i,x) and T(j,t) are Chebyshev Polynomials of the first kind, given by

```
T(0,x) = 1
T(1,x) = x
T(2,x) = 2x^2 - 1
T(3,x) = 4x^3 - 3x.
(2.4.28)
```

When we have constructed a function of this form, it is easy to convert it to a regular polynomial by multiplying out and collecting terms in x and t. A Maple procedure that does this is included on the accompanying CD-ROM.

Applying this to g(x,t) gives

| 1.570994357 | -0.6461396421 | 0.07949824672 | -0.004354110679 |
| 0.5642929825 | 0.5945659091 | -0.1730440015 | 0.01418982936 |
| -0.1783657609 | 0.08610292588 | 0.1079287872 | -0.01567243477 |
| 0.04319948653 | -0.03465102568 | -0.01439451411 | 0.005849053560 |

for best accuracy in 0 < a . b < 1. Clearly, more terms can be used, and each row adds two SIMD instructions and more precision to the x expansion.

One of the most useful features of this method is that once the vector

\(\frac{1}{1+x} \mathbf{XM}\)

is evaluated, multiple \(\alpha(r)\) and \(\beta(r)\) values can be generated with simple algebra.

## Listing 2.4.3 Matrix Slerp Method Class

```
class SlerpMatrix
{
public:
    SlerpMatrix( const Quat &a, const Quat &b ) : mA( a ), mB( b )
    {
        float adotb = a.X * b.X + a.Y * b.Y + a.Z * b.Z + a.W * b.W;
        mRecipOnePlusAdotb = Recip( 1 + adotb );
        mC1 = 1.570994357f + ( -5642929859f + ( -1783657717f
        + 43199498352e-1f * adotb ) * adotb ) * adotb;
        mC3 = - 6461396382f + ( 5945657936f + ( -8610323953e-1f
        - 3465122828e-1f * adotb ) * adotb ) * adotb;
        mC5 = .794982521e-1f + ( - .1730436931f + ( .1079279599f
        - .143997801e-1f * adotb ) * adotb ) * adotb;
        mC7 = - .4354102836e-2f + ( .1418962736e-1f + ( - .1567189691e-1f
        + .5848706227e-2f * adotb ) * adotb ) * adotb;
    }
    Quat Interpolate( float t ) const
    {
        float T = 1 - t, t2 = t * t, T2 = T * T;
        float alpha = ( mC1 + ( mC3 + ( mC5 + mC7 * T2 ) * T2 ) * T2 ) * T *
        mRecipOnePlusAdotb;
        float beta = ( mC1 + ( mC3 + ( mC5 + mC7 * T2 ) * T2 ) * T2 ) * t *
        mRecipOnePlusAdotb;
        return Quat( alpha * mA.X + beta * mB.X, alpha * mA.Y +
        beta * mB.Y, alpha * mA.Z + beta * mB.Z,
        alpha * mA.W + beta * mB.W );
    }
}
}
private:
    float mRecipOnePlusAdotB;
    float mC1, mC3, mC5, mC7;
    const Quat mA;
    const Quat &mB;
};
```

Here, we precalculate polynomial coefficients that enable us to simply calculate a series of interpolations. In practice, we would probably recode this using native SIMD instructions.

## Renormalization

A quick and dirty approximation, where accuracy is not important, is to simply linear interpolate (lerp) the quaternions and renormalize the result. This produces a result that is good to about four to eight bits in normal use, which is quite often enough. If the angle between the quaternions is very small, the result is quite accurate.

This is the method that has been used in vertex shaders as it is possible to blend between several quaternions in a way that is superior to conventional matrix blending.

However, except for the setup time, the interpolation is slower than the Matrix slerp method presented earlier and has significantly less precision.

Listing 2.4.4 shows an implementation.

## Listing 2.4.4 Simple Lerp and Renormalization

```
class SlerpSimpleRenormal
{
public:
    SlerpSimpleRenormal( const Quat &a, const Quat &b ) :
        mA( a ), mB( b )
    {
    }

    Quat Interpolate( float t ) const
    {
        float alpha = 1 - t;
        float beta = t;
        Quat result( alpha * mA.X + beta * mB.X, alpha * mA.Y +
            beta * mB.Y, alpha * mA.Z + beta * mB.Z,
            alpha * mA.W + beta * mB.W );
        float recip = RecipSqrt( result.X * result.X + result.Y *
            result.Y + result.Z * result.Z + result.W * result.W );
        return Quat( result.X * recip, result.Y * recip,
            result.Z * recip, result.W * recip );
    }
}
private:
    const Quat &mA;
    const Quat &mB;
};
```

The simple lerp can be improved by approximating

\(\beta(x,t)=\frac{\sin(\arccos x)}{\sin(\arccos x)+\sin((1-t)\arccos x)}, \alpha(x,t)=1-\beta(x,t), (2.4.31)\)

instead, and then renormalizing. Alternatively, the angle subdivision methods can be used before the lerp and renormalization operations.

Renormalization can also significantly improve the accuracy of the direct and matrix methods, but at the cost of extra time.

Listing 2.4.5 shows an implementation of the improved renormalization method.

## Listing 2.4.5 An Improved Renormalization Method (Rather Cumbersome, However)

```
class SlerpRenormal
{
public:
    SlerpRenormal( const Quat &a, const Quat &b ) :
        mA( a ), mB( b )
    {
        float adotb = a.X * b.X + a.Y * b.Y + a.Z * b.Z + a.W * b.W *
            b.W;

        adotb = Min( adotb, 0.995f );
        float even = 2.218480716f + .2234036692f * adotb * adotb;
        float odd = 2.441884385f * adotb;
        mTheta = Sqrt( even - odd ) * Sqrt( even + odd )
            + 1.570796327f + .639128730f * adotb;
    }
}

Quat Interpolate( float t ) const
{
    float T = 1 - t, t2 = t * t, T2 = T * T;
    float A = ( 1 - t ) * mTheta;
    float B = t * mTheta;
    float sinA = .67044e-5f + ( 1.000271283f + .1621365372f + ( .55809983e-2f +
        - .127120213e-2f * A ) * A ) * A;
    float sinB = .67044e-5f + ( 1.000271283f + .1621365372f + ( .55809983e-2f +
        - .127120213e-2f * B ) * B ) * B;
    float recipAB = Sqrt( sinA * sinB );
    float alpha = sinA * recipAB;
    float beta = sinB * recipAB;
}
// renormalise
Quat result( alpha * mA.X + beta * mB.X, alpha * mA.Y +
beta * mB.Y,
alpha * mA.Z + beta * mB.Z, alpha * mA.W + beta *
mB.W );
float recip = RecipSqrt( result.X * result.X + result.Y *
result.Y +
result.Z * result.Z + result.W * result.W );
return Quat( result.X * recip, result.Y * recip,
result.Z * recip, result.W * recip );
}
private:
float mTheta;
const Quat mA;
const Quat mB;
};
```

## Angle Subdivision Methods

We can bisect the angle between two quaternions by noting that

\(\beta(x, \frac{1}{2}) = \alpha(x, \frac{1}{2}) = \frac{\sin(\frac{1}{2} \arccos(x))}{\sqrt{1-x^2}} = \frac{1}{\sqrt{2+2x}}.\) (2.4.32)

This is exact for half the angle and can be extended for any value of t that is composed of quarters, eighths, sixteenths, and so on. A Maple worksheet is included on the accompanying CD-ROM that calculates the subdivision beta functions in terms of square roots using bisection

![](img/672fe9a2d008ba627b1991e15d70f43e_305_0.png)

\(\beta(x, 0) = 0,\)
\(\beta(x, 1/4) = \frac{1+\sqrt{2+2x}}{\sqrt{2+\sqrt{2+2x}}\sqrt{2+2x}},\)
\(\beta(x, 1/2) = \frac{1}{\sqrt{2+2x}},\)
\(\beta(x, 3/4) = \frac{1}{\sqrt{2+\sqrt{2+2x}}\sqrt{2+2x}},\)
\(\beta(x, 1) = 1.\) (2.4.33)

## Comparison of Methods

We compared the classes for accuracy and speed. The test data were three sets of quaternion encodings with large, medium, and tiny rotations.
