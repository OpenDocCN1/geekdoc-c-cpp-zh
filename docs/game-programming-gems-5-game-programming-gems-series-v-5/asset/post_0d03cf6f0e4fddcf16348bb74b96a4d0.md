
We discuss several methods of approximation and summarize their strengths and weaknesses. One of the golden rules of numerical approximation is that no one method is best. The context in which the approximation is to be used must be considered when determining the specific method.

In computer games, we may have to ask ourselves a number of questions, notably:

- How many CPU cycles can we spare?
- How much precision do we need?
- Can we cheaply use functions such as sqrt(x) and exp(x)?
- Can we use SIMD instructions, like VU macro mode, paired float, SSE, or 3DNow?
- Are we going to be blending more than two quaternions at once?
- What is the maximum angle between our keys?

We present various methods here, but it is up to the reader to decide which is most appropriate for a particular application.

## Direct Method

We start with the direct approach. We just examine the beta function formula and approximate the various components. This is actually the best method if very high precision is necessary, but it can be very costly, especially when evaluating large batches of slerps.

Almost every game engine contains something like the code in Listing 2.4.1, and many games spend significant proportions of their time executing it.

## Listing 2.4.1 Reference Slerp Class

```
class SlerpReference
{
public:
    SlerpReference( const Quat &a, const Quat &b ) : mA( a ),
        mB( b )
    {
        float adotb = a.X * b.X + a.Y * b.Y + a.Z * b.Z + a.W * b.W;
        adotb = Min( adotb, 0.9999f );
        mTheta = acosf( adotb );
        mRecipSqrt = RecipSqrt( 1 - adotb * adotb );
    }

    Quat Interpolate( float t ) const
    {
        float alpha = sinf( ( 1 - t ) * mTheta ) * mRecipSqrt;
        float beta = sinf( t * mTheta ) * mRecipSqrt;
        return Quat( alpha * mA.X + beta * mB.X, alpha * mA.Y +
            beta * mB.Y, alpha * mA.Z + beta * mB.Z,
            alpha * mA.W + beta * mB.W );
    }

private:
    float mTheta;
    float mRecipSqrt;
    const Quat &mA;
    const Quat &mB;
};
```

Here we have used trig functions to create a reference slerp class. The class has a constructor and a method to calculate individual interpolated quaternions. We have taken pains to avoid using branches that could cause lengthy pipeline stalls by using the min function to avoid overflows. Note that although the results near adotb = 1 will be consistent, if the quaternions point away from each other, the result will be unpredictable.

To turn this into an approximation, we have to approximate sin(x) and arccos(x). The sin(x) component is simple, as this responds to traditional polynomial approximation tools. In Maple, there is a package called numapprox that contains polynomial approximation tools that can convert an arbitrary function into a polynomial over a certain range of values.

A Taylor series turns a function of x into a polynomial in x that matches the function exactly at one point. Maple has a built-in Taylor series command that gives a result like this:

taylorseries = x - x³ / 3! + x⁵ / 5! + O(x⁷). (2.4.18)

Unfortunately, Taylor series are not very useful for approximation as they are exact in one place only, but they are simple to calculate and are useful for showing us the general form of a function. A polynomial can be made to be exact in n or more different places, where n is the degree of the polynomial, or highest power term. This can be used to significantly reduce the error.

In the numapprox package, Maple has a command called minimax that chooses the best places to make a polynomial exact in such a way as the maximum error is minimized, hence the name.

minimaxSeries = minimax( sin(x), x = -Pi..Pi, 3 ) = (8245355 + (-08692x)x)x (2.4.19)

Figure 2.4.3 shows a plot of taylorseries, minimaxseries, and sin(x). Here we see that the Taylor series shoots off to infinity when |x| > 1. Figure 2.4.4 shows a plot of the error, which shows that the Taylor series is exact only at the origin, whereas the minimax polynomial is exact in five separate places, spreading out the error over the interval.

![](img/672fe9a2d008ba627b1991e15d70f43e_295_0.png)

![](img/672fe9a2d008ba627b1991e15d70f43e_295_1.png)

This is how the built-in functions in C++ are created. The following is an approximation to cos(x) on the interval x = [-π / 2, π / 2] that we can use to approximate \(\sin(x)\) on \(x \in [0, \pi]\). In this case, \(\cos(x)\) is an easier function to approximate than \(\sin(x)\), as it is even and hence uses only terms in \(x^2\).

```
cos(x) = sin(x + \pi/2) = 1 + (-0.4999991 + (0.0416636 + (-0.00138537 + 0.0000231540*x^2)*x^2)*x^2)*x^2 (2.4.20)
```

**FIGURE 2.4.5** Showing the error in the approximation to \(\cos(x)\) shifted into the range used by the slerp function.

The \(\arccos(x)\) function does not respond to this kind of treatment. Figure 2.4.6 shows a plot of the error for eight terms, which is shockingly bad.

The reason for this can be seen by looking at the \(\arccos\) function itself, shown in Figure 2.4.7. There are singularities at \(x = 1\) and \(x = -1\) that behave as \(\sqrt{1-x}\) and \(\sqrt{1+x}\), respectively. It is very hard for a polynomial to approximate this kind of function. These kinds of behaviors can be discovered using the Maple 'series' command.

Making this approximation in terms of nonlinear terms works much better:

```
arccos(x) =
\sqrt{2.218480716 - 2.441884385x + 0.2234036692x^2 -
\sqrt{2.218480716 + 2.441884385x + 0.2234036692x^2} +
\pi/2 + 0.6391287330x. (2.4.21)
```

![](img/672fe9a2d008ba627b1991e15d70f43e_297_0.png)

**FIGURE 2.4.6** The result of using Maple's minimax on the arccos function.

![](img/672fe9a2d008ba627b1991e15d70f43e_297_1.png)

**FIGURE 2.4.7** A plot of arccos(x) showing singularities at x = ±1.

The error for this approximation to arccos(x) is plotted in Figure 2.4.8. Note that these functions only work over our required range. If functions that work over other ranges are needed, they will have to be made separately. The accompanying CD-ROM contains some example Maple worksheets.

![](img/672fe9a2d008ba627b1991e15d70f43e_298_0.png)

**FIGURE 2.4.8** A better approximation to arccos(x).

The reciprocal square root is available on most modern processors using the division unit. One should be careful to allow for latency, however, and calculate this first so that the result is available later. An approximate reciprocal square root is also often available in a single-cycle form to 16 bits with SIMD instructions.

The proportional error in the rotation can be calculated to be of the same order as the error in the alpha and beta functions. To perform this calculation, we may assume an error \(\epsilon\) in the function and use the Maple “series” command. Decrease the number of series terms until the \(O(\epsilon^i)\) is the last remaining term in \(\epsilon\).

Figure 2.4.9 shows a series of error plots of beta functions for various angles of separation of the quaternions

```
\frac{\sin(t \arccos(x))}{\sqrt{1-x^2}} \frac{\sin(t \arccos x)}{\sqrt{1-x^2}} (2.4.22)
```

Where Sin(x) and Arccos(x) are the approximations.

## Plot of Errors of Various Beta(x,t)

![](img/672fe9a2d008ba627b1991e15d70f43e_299_0.png)

**FIGURE 2.4.9** Plots of errors in $\beta(x,t)$ for various $x$.

Use of SIMD architectures enables the calculation of both sine functions together, as shown in Listing 2.4.2.

## Listing 2.4.2 Direct Slerp Method Class

```
class SlerpDirect
{
public:
    SlerpDirect( const Quat &a, const Quat &b ) : mA( a ), mB( b )
    {
        float adotb = a.X * b.X + a.Y * b.Y + a.Z * b.Z + a.W * b.W;
        adotb = Min( adotb, 0.99999f );
        float even = 2.21840761F + 0.2234036692F * adotb * adotb;
        float odd = 2.441884385F * adotb;
        mTheta = Sqrt( even - odd ) - Sqrt( even + odd ) +
                 1.570796327f + 0.639128730F * adotb;
        mRecipSqrt = RecipSqrt( 1 - adotb * adotb );
    }

    Quat Interpolate( float t ) const
    {
        float A = ( 1 - t ) * mTheta - 1.570796327f; A = A * A;
        float B = t * mTheta - 1.570796327f; B = B * B;
        float sinA = 0.9999999535f*( 0.4999999537f*( 4166358517e-1f
        +( 0.1385370794e-2f+0.2315401401e-4f*A)*A)*A;
```
