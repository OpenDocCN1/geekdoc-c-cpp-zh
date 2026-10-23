of this exercise is to determine if the use of multiprecision data types can remedy this problem. Answer the following questions:

+   a) Apply the explicit Euler method to the ODE (24.46) using multiprecision data types. Is this an improvement to using double?
+   b) Now apply Cash–Karp with multiprecision data types to ODE (24.46) and investigate the potential improvements.
+   c) Depending on the findings from parts a) and b), consider applying Boost odeint to the system (24.51).

Having completed this exercise you should be in a position to give an opinion on the usefulness (or not) of multiprecision data types when computing the numerical solutions of stiff ODEs.

# 2. (Boost odeint for Complex State Types)

Differential equations whose coefficients are complex numbers occur in a number of applications, for example Fourier transforms and the transformation of PDEs to ODEs.

There are two main ways to solve ODEs with complex-valued coefficients. The first approach is to use Boost odeint for complex numbers, as the following simple example shows:

```
// C++ types
using value_type = double;
using state_type = std::complex<value_type>;

namespace Bode = boost::numeric::odeint;

// Global parameters of ODE
std::complex<double> a(2,3);   // 2 + 3i
std::complex<double> A(10,0);  // 10

class OdeExp
{
public:

public:
    OdeExp() { }

    void operator() (const state_type &x, state_type &dxdt,
        const value_type t)
    {
        // C++ standard
        dxdt = -a * x;
    }
};

int main()
{
    namespace Bode = boost::numeric::odeint;

    // Initial condition
    state_type x;
    x = A;
```