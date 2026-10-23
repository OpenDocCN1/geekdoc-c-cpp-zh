```
std::function<double()> m_discounter;

Pricer() = default;
Pricer(const std::function<double(double)>& payoff,
    const std::function<double()>& discounter)
{
    m_payoff = payoff;
    m_discounter = discounter;
}
};

// Pricing Engines
class EuropeanPricer : public Pricer< EuropeanPricer>
{
private:
    // ...

public:
    // Code same as in section 31.4
};
```

and

```
template <typename D> class Rng
{
public:
    double GenerateRn()
    {
        return static_cast<D*>(this)->GenerateRn();
    }
};
```

```
class PolarMarsaglia : public Rng<PolarMarsaglia>
{ // Only for educational purposes

private:
    std::default_random_engine dre;
    std::uniform_real_distribution<double> unif;
    // ...
public:
    // ...
};
```

The code to test this new hierarchy is similar to that in Section 31.4 and we see the emergence of instantiated pricer and random number classes:

```
auto pricerCall = std::shared_ptr<Pricer<EuropeanPricer>>
    (new EuropeanPricer(payoffCall, discounter));
```