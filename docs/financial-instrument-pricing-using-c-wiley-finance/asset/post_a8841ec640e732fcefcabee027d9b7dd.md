
```
const double a2 = -0.1201876;
const double a3 = 0.9372980;

double Cdf_26_2_16(double x)
{ // 26.2.16 O(-5) accurate

double t = 1.0 / (1.0 + p*x);

double Z = std::exp(-0.5*x*x) / SQRT2PI;

return 1.0 - Z*(t * (a1 + t*(a2 + a3*t)));
}
```

Other implementations are possible, such as ‘26.2.17’ (order 8) and ‘26.2.18’ (order 4) and their accuracy can be compared with that of the C++11 implementation (the code is on the distribution medium delivered by the author):

```
// 101 tests of cumulative normal distribution
double x = 2.3;
std::cout << "Cdf_26_2_16 O(5): " << std::setprecision(15)
<< Cdf_26_2_16(x) << '\n';
std::cout << "Cdf_26_2_17 O(8): " << std::setprecision(15)
<< Cdf_26_2_17(x) << '\n';
std::cout << "Cdf_26_2_18 O(4): " << std::setprecision(15)
<< Cdf_26_2_18(x) << '\n';
std::cout << "Cdf C++11 via erfc: " << std::setprecision(15)
<< N(x) << '\n';
```

In the final case we have conveniently defined a function for the cumulative distribution that we use in code (for example, in option pricing formulae):

```
double N(double x)
{ // aka CdfN(x)

return 0.5*std::erfc(-x / std::sqrt(2.0));
}
```

For example, this function can be used in the Black–Scholes formula to price a call option that we also discuss in this chapter.

## 15.2.2 Applications of the Error Function

Our main interest in the error function lies in the ability to recover the cumulative distribution function. It is similar to a probability in the sense that its integral on the real line is one:

1/√π ∫_{-∞}^{∞} e^{-t²} dt = 1. (15.5)

The cumulative function plays an important role in computational finance. For completeness, we show how the error function arises when looking for the solution of PDEs. To this end, we discuss the initial value problem for the one-dimensional heat equation on the positive semi-infinite interval:

\[\frac{\partial u}{\partial t}=a^2\frac{\partial^2u}{\partial x^2},\quad 0<x<\infty,\ t>0\]
\[u(x,0)=f(x),\quad 0\leq x<\infty.\tag{15.6}\]

An analytical solution to this problem can be found using Laplace or Fourier transform methods (see Stakgold, 1998). In the case of constant initial condition \(f(x)=u_0\) the solution becomes:

\[u(x,t)=u_0\operatorname{erf}\left(\frac{x}{2a\sqrt{t}}\right).\tag{15.7}\]

Then we can solve system (15.6) by using the C++11 error function. For the case of non-constant initial condition (payoff), see Exercise 1 in the context of the Black–Scholes PDE.

## 15.3 ONE-FACTOR PLAIN OPTIONS

In this section we discuss the Black–Scholes formula to price one-factor plain put and call options. A full discussion is given in Haug (2007) and the focus here is on examining the formula from a number of perspectives:

- Testing the accuracy of the C++ error function. We implement the cumulative normal distribution in terms of the error function and we test if expected results are produced.
- Generating option call prices. We compare option prices produced by the finite difference method with the exact prices.
- Introducing a number of design patterns (GOF, 1995) that are useful in the current context.
- Events, notification and callbacks.

We introduce the generalised Black–Scholes formula to calculate the price of a call option on an underlying asset. In general, the call price is a function:

\[C=C(S,\ K,\ T,\ r,\ \sigma)\tag{15.8}\]

where:

\(S\) = asset price
\(K\) = strike (exercise) price
\(T\) = exercise (maturity) date
\(r\) = risk-free interest rate
\(\sigma\) = constant volatility.

We can view the call option price C as a function because it maps a vector of parameters into a real value. The well-known exact formula for C is given by:

```
C = S e^{(b - r)T} N(d1) - K e^{-rT} N(d2)  (15.9)
```

where N(x) is the standard cumulative normal (Gaussian) distribution function defined by:

```
N(x) = 1/√(2π) ∫_{-∞}^{x} e^{-y²/2} dy  (15.10)
```

and where:

```
d1 = [log(S/K) + (b + σ²/2)T] / (σ√T)
d2 = [log(S/K) + (b - σ²/2)T] / (σ√T) = d1 - σ√T.  (15.11)
```

The cost-of-carry parameter b has specific values depending on the kind of security (Haug, 2007):

- b = r is the Black–Scholes stock option model
- b = r − q is the Merton model with continuous dividend yield q
- b = 0 is the Black–Scholes futures option model
- b = r − R is the Garman and Kohlhagen currency option model, where R is the foreign risk-free interest rate.

Since we are mainly interested in computing option prices and their sensitivities, we have decided to design the software here using the Command design pattern based on subtype polymorphism in combination with a class hierarchy (GOF, 1995). The definition is:

> Command is a behavioural design pattern in which an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

In the current case each dedicated object computes either an option price or one of its greeks. The corresponding UML diagram is shown in Figure 15.2 for the case of call options, for convenience (the case of put options as well as option vega, rho and theta have been left out). We note the presence of a composite command class that can contain other commands. In this way we can create trees and recursive aggregates of commands. Finally, each command (when executed) sends its result to a Receiver object which in the current case is the console but it could be adapted to other receivers such as another algorithm, Excel or a remote API. Composite receivers are also possible. In this case the event is multicasted to several receivers.

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_490_0.png)

**FIGURE 15.2** Commands for call and put options

This kind of functionality is supported in the *Boost C++ Signals2* library (see Demming and Duffy, 2010).

We now discuss how we designed the configuration from Figure 15.2 in C++. The design is based on subtype polymorphism:

```cpp
class OptionCommand
{
private:

protected:
    double K;    double T; double r; double b; double sig;

public:
    OptionCommand() = default;

    explicit OptionCommand(double strike, double expiration,
                           double riskFree, double costOfCarry, double
                           volatility)
        : K(strike), T(expiration), r(riskFree),
          b(costOfCarry), sig(volatility) {}

    // Want to forbid copy constructor and assignment operator
    OptionCommand(const OptionCommand& c) = delete;
    OptionCommand& operator = (const OptionCommand& c) = delete;

    // The abstract interface
    virtual void execute(double S) = 0;

    // Implement as function object; example of Template Method Pattern
    virtual void operator () (double S)
    {
        // Call derived class' execute()
        execute(S);
    }
};
```

We see that this class is also a function object because it implements the *function call operator* whose implementation is an example of the *Template Method* design pattern

(GOF, 1995). We now reduce the scope by concentrating on call option price, delta and gamma. The three derived classes are:

```
class CallPrice final : public OptionCommand
{
public:
    explicit CallPrice(double strike, double expiration, double riskFree,
                    double costOfCarry, double volatility)
        : OptionCommand(strike, expiration, riskFree, costOfCarry,
        volatility) {}

    virtual void execute(double S) override
    {
        double tmp = sig * std::sqrt(T);
        double d1 = (std::log(S / K) + (b + (sig*sig)*0.5) * T) / tmp;
        double d2 = d1 - tmp;

        std::cout << "Call Price: " <<
            (S * std::exp((b - r)*T) * N(d1)) (K * std:::
            exp(-r * T)* N(d2))
            << '\n';
    }
};

class CallDelta final : public OptionCommand
{
public:
    explicit CallDelta(double strike, double expiration, double riskFree,
                    double costOfCarry, double volatility)
        : OptionCommand(strike, expiration, riskFree, costOfCarry,
        volatility) {}

    virtual void execute(double S) override
    {
        double tmp = sig * std::sqrt(T);
        double d1 = (std::log(S / K) + (b + (sig*sig)*0.5) * T) / tmp;

        std::cout << "Call delta: " << std::exp((b - r)*T) * N(d1) << '\n';
    }
};

class CallGamma final : public OptionCommand
{
public:
    explicit CallGamma(double strike, double expiration, double riskFree,
                    double costOfCarry, double volatility)
        : OptionCommand(strike, expiration, riskFree, costOfCarry,
        volatility) {}

    virtual void execute(double S) override
{
```
