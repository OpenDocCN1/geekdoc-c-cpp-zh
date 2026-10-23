```
private:
    double mp;                  // Market price
    IPricingFunction pricer;    // Call or put price
public:
    ImpliedVolatilityEstimator
        (double marketPrice, const IPricingFunction& optionPricer)
        : mp(marketPrice), pricer(optionPricer) {}

    double operator () (double sig) const
    { // Compute current residual

        double calculatedValue = pricer(sig);
        double d = -mp + calculatedValue;

        // Least-squares form
        return d*d;
    }
};
```

In general, we use this class with well-known pricers:

```
class Pricer
{ // Special adapter class to work with implied volatility
private:
    OptionData opt;
public:
    Pricer(const OptionData& optionData) : opt(optionData) {}

    double PutPrice(double sig) const
    {
        double tmp = sig * std::sqrt(opt.T);

        double d1 = (std::log(opt.S / opt.K)
                    + (opt.b + (sig*sig)*0.5) * opt.T) / tmp;
        double d2 = d1 - tmp;

        return opt.K * std::exp(-opt.r * opt.T)* N(-d2)
               - opt.S* std::exp((opt.b - opt.r)*opt.T) * N(-d1);
    }

    double CallPrice(double sig) const
    {
        double tmp = sig * std::sqrt(opt.T);

        double d1 = (std::log(opt.S / opt.K)
                    + (opt.b + (sig*sig)*0.5) * opt.T) / tmp;
        double d2 = d1 - tmp;
```