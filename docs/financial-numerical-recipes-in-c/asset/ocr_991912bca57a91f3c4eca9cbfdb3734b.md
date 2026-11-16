```
double bonds.convexity(const vector<double>& cashflow.times,
                     const vector<double>& cashflow.amounts,
                     const term.structure.class& d);
// Futures pricing
double futures.price(const double& S, const double& r, const double& time.to.maturity);
```

```
// Binomial option pricing
// one period binomial
double option.price.call.european.binomial.single.period( const double& S, const double& K, const double& r,
                                                          const double& u, const double& d);
// multiple period binomial
double option.price.call.european.binomial.multi.period.given.ud( const double& S, const double& K, const double& r,
                                                                  const double& u, const double& d, const int& no.periods);
// multiple period binomial > vector< vector<double> > binomial.tree(const double& S0, const double& u, const double& d,
                                                                   const int& no.steps);
```

```
// Black Scholes formula////////////////////////////////////////////////////////////////////////////////
double option.price.call.black.scholes(const double& S, const double& K, const double& r,
                                       const double& sigma, const double& time );
double option.price.put.black.scholes(const double& S, const double& K, const double& r,
                                      const double& sigma, const double& time );
double
option.price.implied.volatility.call.black.scholes.newton( const double& S, const double& K,
                                                           const double& r, const double& time,
                                                           const double& option.price);
double
option.price.implied.volatility.put.black.scholes.newton( const double& S, const double& K,
                                                          const double& r, const double& time,
                                                          const double& option.price);
double option.price.implied.volatility.call.black.scholes.bisections( const double& S, const double& K,
                                                                      const double& r, const double& time,
                                                                      const double& option.price);
double option.price.implied.volatility.put.black.scholes.bisections( const double& S, const double& K,
                                                                     const double& r, const double& time,
                                                                     const double& option.price);
double option.price.delta.call.black.scholes(const double& S, const double& K, const double& r,
                                             const double& sigma, const double& time );
double option.price.delta.put.black.scholes( const double& S, const double& K, const double& r,
                                           const double& sigma, const double& time );
void option.price.partials.call.black.scholes(const double& S, const double& K, const double& r,
                                              const double& sigma, const double& time,
                                              double& Delta, double& Gamma, double& Theta,
                                              double& Vega, double& Rho);
void option.price.partials.put.black.scholes(const double& S, const double& K, const double& r,
                                             const double& sigma, const double& time,
                                             double& Delta, double& Gamma, double& Theta,
                                             double& Vega, double& Rho);
```

```
// warrant price
double warrant.price.adjusted.black.scholes(const double& S, const double& K,
                                            const double& r, const double& sigma,
                                            const double& time,
                                            const double& no.warrants.outstanding,
                                            const double& no.shares.outstanding);
double warrant.price.adjusted.black.scholes(const double& S, const double& K,
                                            const double& r, const double& q,
                                            const double& sigma, const double& time,
                                            const double& no.warrants.outstanding,
```