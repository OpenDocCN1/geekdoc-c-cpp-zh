It is possible to differentiate the call price C with respect to any of the parameters to produce a formula for option sensitivities. For example, some differentiation allows us to show that in the case of call options:

Δ_C ≡ ∂C/∂S = e^{(b−r)T} N(d₁)

Γ_C ≡ ∂²C/∂S² = ∂Δ_C/∂S = [n(d₁) e^{(b−r)T}] / [S σ √T]

Vega_C ≡ ∂C/∂σ = S √T e^{(b−r)T} n(d₁)

Θ_C ≡ −∂C/∂T = −[S σ e^{(b−r)T} n(d₁)] / [2 √T] − (b − r) S e^{(b−r)T} N(d₁) − r K e^{−rT} N(d₂).  (15.12)

We can also carry out the same exercise for delta and gamma as follows:

```
void DisplayCallDelta()
{ // Cox and Rubinstein 1985 Figure 5-12

    double K = 50.0;
    double T = 0.4;
    double r = 0.0106;
    double b = r;
    double sig = 0.3;

    // Use lambda function for convenience
    auto callDelta = [&](double S)
    {
        double tmp = sig * std::sqrt(T);
        double d1 = (std::log(S / K) + (b + (sig*sig)*0.5) * T) / tmp;

        return std::exp((b - r)*T) * N(d1);
    };

    std::size_t N = 100;
    std::vector<double> S(N);
    std::vector<double> C(S.size());

    // Generate array of underlyings
    double startS = 5.0;
    std::iota(std::begin(S), std::end(S), startS);

    for (std::size_t i = 0; i < S.size(); ++i)
    {
        C[i] = callDelta(S[i]);
    }
```