```
return S * std::exp((b-r)*T)*n(d1) * sqrt(T);
}
```

```
// The rhs of x' = f(x) defined as a class
class Davidenko
{
private:
    state_type x0;

public:
    Davidenko(state_type guess) : x0(guess) {}
    void operator() (const state_type& x, state_type& dxdt,
        const value_type t)
    {
        dxdt[0] = -Function(x0) / FunctionDeriv(x);
    }
};
```

A test program is:

```
typedef double value_type;
typedef std::vector<value_type> state_type;

int main()
{
    namespace Bode = boost::numeric::odeint;

    // Initial condition
    state_type x(1, 0.0); // vector
    x[0] = 0.113;

    Davidenko ode(x);

    value_type L = 0.0;
    value_type U = 1.0; // upper limit
    value_type dt = 1.0e-9;

    std::size_t steps = Bode::integrate(ode, x, L, U, dt);
    std::cout << "Value from 101 integrator: "
              << std::setprecision(8)  << x[0] << std::endl;

    Bode::runge_kutta_dopri5<state_type, value_type> myStepper;

    x[0] = 0.113;
    dt = 1.0e-1;
    int n = static_cast<int>((U - L)/dt);
```