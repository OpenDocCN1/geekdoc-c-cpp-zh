
We focus on four cases as motivation to show how to use the code:

- Two-asset correlation options.
- Minimum of two risky assets (Haug, 2007, p. 211).
- Best-or-worst cash-or-nothing (from Haug, 2007, p. 224).
- Two-asset cash-or-nothing options (four types) (Haug, 2007, p. 221).

The resulting C++ code is relatively straightforward and it is a direct mapping from the algorithms in Haug (2007). The added value in this context is that we have several efficient and accurate methods to compute integral (16.1). We show the code without further comment as it is relatively straightforward:

```
int main()
{

    double a = 8.5; double b = 8.5; double Rho = 0.0;
    std::cout << M(a,b,Rho) << std::endl;
    {
        // 2-asset correlation option (Haug 2007)
        double S1 = 52.0; double S2 = 65.0;
        double T = 0.5;
        double K1 = 50.0; double K2 = 70.0;
        double s1 = 0.2; double s2 = 0.3;
        double r = 0.1;
        double b1 = 0.1; double b2 = 0.1;
        double rho = 0.75;

        // Other variables
        double y1 = (std::log(S1/K1) + (b1 - s1*s1/2)*T) / (s1*sqrt(T));
        double y2 = (std::log(S2/K2) + (b2 - s2*s2/2)*T) / (s2*sqrt(T));

        // 2-asset correlation options
        double call = S2*std::exp((b2-r)*T)*M(y2 + s2*sqrt(T), 1
                     + rho*s2*sqrt(T), rho)
                     - K2*std::exp(-r*T)*M(y2,y1,rho);
        std::cout << "Call correlation: " << call << std::endl;

        double put = K2*std::exp(-r*T)*M(-y2, -y1, rho)
                   - S2*std::exp((b2-r)*T)*M(-y2-s2*sqrt(T),
                     -y1-rho*s2*sqrt(T),rho);
        std::cout << "Put correlation: " << put << std::endl;
    }

    // Minimum of two risky assets (Haug 2007, page 211)
    {
    /* double S1 = 100.0; double S2 = 105.0;
double T = 0.5;
double K = 98.0;
double s1 = 0.11; double s2 = 0.16;
double r = 0.05;
double b1 = 0; double b2 = 0; // Investigate b < 0
double rho = 0.63;*/

double S1 = 85.0; double S2 = 60.0;
double T = 2.0;
double K = 100.0;
double s1 = 0.40; double s2 = 0.25;
double r = 0.08;
double b1 = r; double b2 = r; // Investigate b < 0
double rho = -0.70;

// Other variables
double s = std::sqrt(s1*s1 + s2*s2 - 2.0*rho*s1*s2);
double d = (std::log(S1/S2) + (b1 - b2 + s*s/2)*T)
    / (s*std::sqrt(T));

double y1 = (std::log(S1/K) + (b1 + s1*s1/2)*T) / (s1*sqrt(T));
double y2 = (std::log(S2/K) + (b2 + s2*s2/2)*T) / (s2*sqrt(T));

double rho1 = (s1 - rho*s2)/s;
double rho2 = (s2 - rho*s1)/s;

// As a function of S1,S2,K,T
double cMinK =
    S1*std::exp((b1-r)*T)*M(y1,-d,-rho1)
  + S2*std::exp((b2-r)*T)*M(y2,d-s*std::sqrt(T), -rho2)
  - K*std::exp(-r*T)
  *M(y1 - s1*std::sqrt(T), y2 - s2*std::sqrt(T), rho);
std::cout << "Call min K: " << cMinK << std::endl;

double cMaxK =
    S1*std::exp((b1-r)*T)*M(y1,d,rho1)
  + S2*std::exp((b2-r)*T)*M(y2,-d+s*std::sqrt(T), rho2)
  - K*std::exp(-r*T)*(1.0 - M(-y1 + s1*std::sqrt(T), -y2
  + s2*std::sqrt(T), rho));
std::cout << "Call max K: " << cMaxK << std::endl;
}

// Best-or-worst cash-or-nothing (Haug 2007 page 224)
{
 double S1 = 105.0; double S2 = 100.0;
 double T = 0.5;
 double Q = 5.0;
 double s1 = 0.3; double s2 = 0.2;
 double r = 0.08;
 double b1 = 0.06; double b2 = 0.02;
double rho = 0.75;

double K = 100.0;

// Other variables
double s = std::sqrt(s1*s1 + s2*s2 - 2.0*rho*s1*s2);
double y = (std::log(S1/S2) + (b1 - b2 + s*s/2)*T)
    / (s*std::sqrt(T));

double z1 = (std::log(S1/K) + (b1 + s1*s1/2)*T)
    / (s1*std::sqrt(T));
double z2 = (std::log(S2/K) + (b2 + s2*s2/2)*T)
    / (s2*std::sqrt(T));

double rho1 = (s1 - rho*s2)/s;
double rho2 = (s2 - rho*s1)/s;

// As a function of S1,S2,K,T
double cBest = Q*std::exp(-r*T)*(M(y,z1,-rho1) + M(-y,z2,-rho2));
std::cout << "Call worst cash-or-nothing best: "
    << cBest << std::endl;
}

// 2-asset cash-or-nothing options (4 types) (Haug 2007 page 221)
{
    double S1 = 100.0; double S2 = 100.0;
    double K1 = 110.0; double K2 = 90.0;
    double T = 0.5;
    double Q = 10.0;
    double s1 = 0.2; double s2 = 0.25;
    double r = 0.1;
    double b1 = 0.05; double b2 = 0.06;
    double rho = 0.5;

    double d11 = (std::log(S1/K1) + (b1 - s1*s1/2)*T)
        / (s1*std::sqrt(T));
    double d12 = (std::log(S1/K2) + (b1 - s1*s1/2)*T)
        / (s1*std::sqrt(T));
    double d21 = (std::log(S2/K1) + (b2 - s2*s2/2)*T)
        / (s2*std::sqrt(T));
    double d22 = (std::log(S2/K2) + (b2 - s2*s2/2)*T)
        / (s2*std::sqrt(T));

    double cType1 = Q*std::exp(-r*T)*M(d11,d22,rho);
    double cType2 = Q*std::exp(-r*T)*M(-d11,-d22,rho);
    double cType3 = Q*std::exp(-r*T)*M(d11,-d22,-rho);
    double cType4 = Q*std::exp(-r*T)*M(-d11,d22,-rho);

    std::cout << "Two-asset cash-or-nothing types: " << std::endl;
    std::cout << "Type 1: " << cType1 << std::endl;
    std::cout << "Type 2: " << cType2 << std::endl;
    std::cout << "Type 3: " << cType3 << std::endl;
    std::cout << "Type 4: " << cType4 << std::endl;
}

return 0;
}
```

We tested these algorithms using the Genz/West code:

```
double M(double a, double b, double rho)
{
    return bivarcumnorm(a, b, rho);
}
```

The output is:

```
Call correlation: 4.707330012666851
Put correlation: 3.909280147364093
Call min K: 0.0180004745810719
Call max K: 20.94494846250169
Call worst cash-or-nothing best: 2.793935852582142
Two-asset cash-or-nothing types:
Type 1: 2.498749451519521
Type 2: 2.156694921716584
Type 3: 0.2128123872130617
Type 4: 4.644037484557975
```

We now price these options using the extrapolated version of the finite difference scheme:

```
double M(double a, double b, double rho)
{
    using value_type = double;

    std::size_t NX = 50;    std::size_t NY = 50;
    value_type AL = -8.0; value_type BL = -8.0;
    auto xarr = CreateMesh(NX, AL, a);
    auto yarr = CreateMesh(NY, BL, b);

    BVNFunction<value_type> bvn(rho);
    GoursatFdmExtrapolation<value_type> fdm(AL, BL, bvn, NX, NY);

    return fdm(a, b);
}
```

The output in this case is:

```
Call correlation: 4.707325487726628
Put correlation: 3.909281409246201
Call min K: 0.01787816522478947
Call max K: 20.9451108618852
Call worst cash-or-nothing best: 2.793934246406374
Two-asset cash-or-nothing types:
Type 1: 2.498749988890371
Type 2: 2.156695455034736
Type 3: 0.2128125164628895
Type 4: 4.644034994433958
```

We increase the number of subintervals to 500 and the output in this case becomes:

```
Call correlation: 4.70733001221495
Put correlation: 3.909280147488811
Call min K: 0.01800046275512779
Call max K: 20.94494847804961
Call worst cash-or-nothing best: 2.793935852422795
Two-asset cash-or-nothing types:
Type 1: 2.498749451572514
Type 2: 2.156694921769651
Type 3: 0.2128123872261226
Type 4: 4.644037484309941
```

As expected, the accuracy of the finite difference schemes improves as we increase the number of subdivisions of the domain of integration. You can experiment with the code in order to test other two-asset problems.

## 16.9 TRIVARIATE NORMAL DISTRIBUTION

We conclude this chapter with a discussion on the computation of the trivariate cumulative normal distribution (called TVN for short) using both the Genz algorithm and the generalisation of the PDE (16.2) and finite difference scheme (16.6) to three dimensions. We discuss the implementation of the Genz algorithm as described in West (2004) and compare its accuracy with that produced by our finite difference scheme.

The trivariate normal distribution has its cumulative distribution function defined by:

```
N(b1, b2, b3; Σ) = 1/((2π)^{3/2} √|Σ|) ∫_{-∞}^{b1} ∫_{-∞}^{b2} ∫_{-∞}^{b3} f(x, y, z; Σ) dz dy dx   (16.12)
```

where Σ is the positive-definite covariance matrix and |Σ| is its determinant:

```
Σ = ⎛ 1   ρ12  ρ13 ⎞
    ⎜ ρ12  1   ρ23 ⎟
    ⎝ ρ13  ρ23  1  ⎠

f(x, y, z; Σ) = exp( -½ wᵀ Σ⁻¹ w ),   w = (x, y, z)ᵀ
```

and Σ⁻¹ is the inverse of Σ.

We have implemented this function in C++ by explicitly computing the inverse of the covariance matrix. We also used a more explicit form for the probability density function:

```
f(b1, b2, b3; Σ) = exp(-w/q) / ((2π)^{3/2} √[1 − (ρ12² + ρ13² + ρ23²) + 2ρ12ρ13ρ23])   (16.13)
```

where:

```
q = 2(ρ12² + ρ13² + ρ23² − 2ρ12ρ13ρ23 − 1)
w = b1²(ρ23² − 1) + b2²(ρ13² − 1) + b3²(ρ12² − 1)
  + 2[b1b2(ρ12 − ρ13ρ23) + b1b3(ρ13 − ρ12ρ23) + b2b3(ρ23 − ρ12ρ13)]
```

The code for this function is:

```
double f(double x, double y, double z, double a12, double a13, double a23)
{
    double q = 2.0*(a12*a12 + a13*a13 + a23*a23 - 2.0*a12*a13*a23 - 1.0);

    // Covariance matrix must be positive semi-definite
    double tmp = 1.0 - (a12*a12 + a13*a13 + a23*a23) + 2.0*a12*a13*a23;
    if (tmp <= 0.0)
        return std::numeric_limits<double>::max();

    double fac = std::sqrt(tmp);

    double fac2 = 2.0*std::sqrt(2.0)*std::pow(3.14159, 1.5);
    // x = b1, y = b2, z = b3

    double w = x*x*(a23*a23 - 1.0) + y*y*(a13*a13 - 1.0) + z*z*(a12*a12 - 1.0)
        + 2.0*(x*y*(a12 - a13*a23) + x*z*(a13 - a12*a23) + y*z*(a23 - a12*a13));

    return std::exp(-w / q) / (fac2 * fac);
}
```

When testing the finite difference code we used both forms for the probability density function when computing the integral in equation (16.12).

Similar to the two-dimensional case we can differentiate the integral to produce a third-order hyperbolic PDE:

∂³u / ∂x∂y∂z = f.  (16.14)

We solve (16.14) by a finite difference method that is the three-dimensional analogue of scheme (16.6):

V_{i,j,k} = V_{i-1,j,k} + V_{i,j-1,k} − V_{i-1,j-1,k} + V_{i,j,k-1} − V_{i-1,j,k-1} − V_{i,j-1,k-1} + V_{i-1,j-1,k-1} + h_x h_y h_z f_{i-1/2,j-1/2,k-1/2}  (16.15)
