# Plot of Errors of Various Beta(x,t)

![](bbox=[0.15, 0.1, 0.9, 0.42])

FIGURE 2.4.9 Plots of errors in $\beta(x,t)$ for various $x$.

Use of SIMD architectures enables the calculation of both sine functions together, as shown in Listing 2.4.2.

# Listing 2.4.2 Direct Serp Method Class

```
class SerpDirect
{
public:
    SerpDirect( const Quat &a, const Quat &b ) : mA( a ), mB( b )
    {
        float adotb = a.X * b.X + a.Y * b.Y + a.Z * b.Z + a.W * b.W;
        adotb = Min( adotb, 0.99999f );
        float even = 2.21840761F + , 2234036692F * adotb * adotb;
        float odd = 2.441884385F * adotb;
        mTheta = Sqrt( even - odd ) - Sqrt( even + odd ) +
                 1.570796327f + .639128730F * adotb;
        mRecipSqrt = RecipSqrt( 1 - adotb * adotb );
    }

    Quat Interpolate( float t ) const
    {
        float A = ( 1 - t ) * mTheta - 1.570796327f; A = A * A;
        float B = t * mTheta - 1.570796327f; B = B * B;
        float sinA = .9999999535f*( .4999999537f*( 4166358517e-1f
        +( .1385370794e-2f+.2315401401e-4f*A)*A)*A;
```