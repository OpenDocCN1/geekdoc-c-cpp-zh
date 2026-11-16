
```cpp
const double& q);
double interest_rate_trees_gbm_value_of_callable_bond(const vector<double>& cflows,
    const vector< vector<double> >& r_tree,
    const double& q,
    const int& first_call_time,
    const double& call_price);
double price_european_call_option_on_bond_using_ho_lee(term_structure_class* initial,
    const double& delta,
    const double& pi,
    const vector<double>& underlying_bond_cflow_times,
    const vector<double>& underlying_bond_cflows,
    const double& K,
    const double& option_time_to_maturity);
```

```cpp
////////////////////////////////////////////
// ho and lee modelling
class term_structure_class_ho_lee : public term_structure_class {
private:
    term_structure_class* initial_term_;
    int n_;
    int l_;
    double delta_;
    double pi_;
public:
    term_structure_class_ho_lee(term_structure_class* fitted_term,
        const int & n,
        const int & l,
        const double& lambda,
        const double& pi);
    double d(const double& T) const;
};
```

```cpp
vector< vector<term_structure_class_ho_lee > >
term_structure_ho_lee_build_term_structure_tree(term_structure_class* initial,
    const int& no_steps,
    const double& delta,
    const double& pi);
double price_european_call_option_on_bond_using_ho_lee(term_structure_class* initial,
    const double& delta,
    const double& pi,
    const vector<double>& underlying_bond_cflow_times,
    const vector<double>& underlying_bond_cflows,
    const double& K,
    const double& option_time_to_maturity);
```

```cpp
////////////////////////////////////////////
// term structure derivatives, analytical solutions
double bond_option_price_call_zero_vasicek(const double& X, const double& r,
    const double& option_time_to_maturity,
    const double& bond_time_to_maturity,
    const double& a, const double& b, const double& sigma);
double bond_option_price_put_zero_vasicek(const double& X, const double& r,
    const double& option_time_to_maturity,
    const double& bond_time_to_maturity,
    const double& a, const double& b, const double& sigma);
#endif
```

## Appendix E

The routines discussed in the book are available for download.

### E.1 Source availability

The algorithms are available from my home page as a ZIP file containing the source code. These have been tested with the latest version of the GNU C++ compiler. As the algorithms in places uses code from the Standard Template Library, other compilers may not be able to compile all the files directly. If your compiler complains about missing header files you may want to check if the STL header files have different names on your system. The algorithm files comply with the current ANSI standard for C++ libraries. If the compiler is more than a couple of years old, it will not have STL. Alternatively, the GNU compiler gcc is available for free on the internet, for most current operating systems.

## List of C++ Codes

| Code | Description | Page |
|------|-------------|------|
| 1.1 | A complete program | 9 |
| 1.2 | Basic operations for the date class | 12 |
| 1.3 | Comparison operators for the date class | 13 |
| 1.4 | Iterative operators for the date class | 14 |
| 3.1 | Present value with discrete compounding | 27 |
| 3.2 | Estimation of the internal rate of return | 31 |
| 3.3 | Test for uniqueness of IRR | 33 |
| 3.4 | Present value calculation with continuously compounded interest | 35 |
| 4.1 | Bond price calculation with discrete, annual compounding | 38 |
| 4.2 | Bond yield calculation with discrete, annual compounding | 39 |
| 4.3 | Bond duration using discrete, annual compounding and a flat term structure | 41 |
| 4.4 | Calculating the Macaulay duration of a bond | 42 |
| 4.5 | Modified duration | 43 |
| 4.6 | Bond convexity with a flat term structure and annual compounding | 44 |
| 4.7 | Bond price calculation with continuously compounded interest and a flat term structure | 47 |
| 4.8 | Bond duration calculation with continuously compounded interest and a flat term structure | 48 |
| 4.9 | Calculating the Macaulay duration of a bond with continuously compounded interest and a flat term structure | 48 |
| 4.10 | Bond convexity calculation with continuously compounded interest and a flat term structure | 48 |
| 5.1 | Term structure transformations | 53 |
| 5.2 | Default code for transformations between discount factors, spot rates and forward rates in a term structure class | 56 |
| 5.3 | Implementing term structure class using a flat term structure | 57 |
| 5.4 | Interpolated term structure from spot rates | 60 |
| 5.5 | Term structure class using linear interpolation between spot rates | 62 |
| 5.6 | Pricing a bond with a term structure class | 64 |
| 5.7 | Calculating a bond's duration with a term structure class | 65 |
| 5.8 | Calculating a bond's convexity with a term structure class | 65 |
| 6.1 | Mean variance calculations using IT++ | 77 |
| 6.2 | Mean variance calculations using Newmat | 78 |
| 6.3 | Calculating the unconstrained frontier portfolio given an expected return using Newmat | 79 |
| 6.4 | Calculating the unconstrained frontier portfolio given an expected return using IT++ | 80 |
| 7.1 | Futures price | 81 |
| 8.1 | Binomial European, one period | 84 |
| 8.2 | Building a binomial tree | 87 |
| 8.3 | Binomial multiperiod pricing of European call option | 88 |
| 9.1 | Price of European call option using the Black-Scholes formula | 90 |
| 9.2 | Calculating the delta of the Black-Scholes call option price | 94 |
| 9.3 | Calculating the partial derivatives of a Black-Scholes call option | 95 |
| 9.4 | Calculation of implied volatility of Black-Scholes using bisections | 96 |
| 9.5 | Calculation of implied volatility of Black-Scholes using Newton-Raphson | 97 |
| 10.1 | Adjusted Black-Scholes value for a Warrant | 101 |
| 11.1 | Option price, continuous payout from underlying | 103 |
| 11.2 | European option price, dividend paying stock | 104 |
| 11.3 | Option price, Roll-Geske-Whaley call formula for dividend paying stock | 107 |
| 11.4 | Price of European Call option on Futures contract | 108 |
| 11.5 | European Futures Call option on currency | 109 |
| 11.6 | Price for an American perpetual call option | 110 |
| 12.1 | Option price for binomial European | 114 |
| 12.2 | Price of American call option using a binomial approximation | 115 |
| 12.3 | Delta | 120 |
| 12.4 | Hedge parameters | 121 |
| 12.5 | Binomial option price with continuous payout | 123 |
| 12.6 | Binomial option price of stock option where stock pays proportional dividends | 125 |
| 12.7 | Binomial option price of stock option where stock pays discrete dividends | 127 |
| 12.8 | Pricing an American call on an option on futures using a binomial approximation | 129 |
| 12.9 | Pricing an American call on an option on currency using a binomial approximation | 130 |
| 13.1 | Explicit finite differences calculation of European put option | 133 |
| 13.2 | Explicit finite differences calculation of American put option | 134 |
| 13.3 | Calculation of price of American put using implicit finite differences with the Newmat matrix library | 138 |
| 13.4 | Calculation of price of American put using implicit finite differences with the IT++ matrix library | 139 |
| 13.5 | Calculation of price of European put using implicit finite differences | 140 |
| 14.1 | Simulating a lognormally distributed random variable | 143 |
| 14.2 | European Call option priced by simulation | 144 |
| 14.3 | Estimate Delta of European Call option priced by Monte Carlo | 145 |
| 14.4 | Payoff call and put options | 146 |
| 14.5 | Generic simulation pricing | 146 |
| 14.6 | Generic with control variate | 148 |
| 14.7 | Generic with antithetic variates | 149 |
| 14.8 | Payoff binary options | 151 |
| 15.1 | The Johnson (1983) approximation to an American put price | 155 |
| 15.2 | Geske Johnson approximation of American put | 158 |
| 15.3 | Barone-Adesi quadratic approximation to the price of a call option | 161 |
| 15.4 | Approximation of American Call due to Bjerksund and Stensland (1993) | 164 |
| 15.5 | Approximation of American put due to Bjerksund and Stensland (1993) | 164 |
| 16.1 | Binomial approximation to Bermudan put option | 168 |
| 16.2 | Analytical price of an Asian geometric average price call | 169 |
| 16.3 | Price of lookback call option | 170 |
| 16.4 | Simulating a sequence of lognormally distributed variables | 173 |
| 16.5 | Generic routine for pricing European options | 173 |
| 16.6 | Payoff function for Asian call option | 174 |
| 16.7 | Payoff function for lookback option | 174 |
| 16.8 | Control Variate | 175 |
| 17.1 | Binomial price of American Call | 178 |
| 17.2 | Generic binomial calculation | 179 |
| 17.3 | Payoff definitions for put and call options | 180 |
| 17.4 | Payoff definitions for binomial options | 181 |
| 17.5 | Generic binomial calculation of delta | 182 |
| 18.1 | Price of American put using a trinomial tree | 184 |
| 19.1 | Merton's jump diffusion formula | 187 |
| 19.2 | Heston's pricing formula for a stochastic volatility model | 190 |
| 20.1 | Black-Scholes for European put option on zero coupon bond | 191 |
| 20.2 | Black-Scholes for European put option on coupon bond | 192 |
| 20.3 | Binomial approximation to American put bond option price | 193 |
| 22.1 | Calculation of the Nelson and Siegel (1987) term structure model | 198 |
| 22.2 | Defining a term structure class wrapper for the Nelson Siegel approximation | 199 |
| 22.3 | Calculation of Svensson's extended Nelson and Siegel (1987) term structure model | 201 |
| 22.4 | Defining a term structure class wrapper for the Svensson model | 201 |
| 22.5 | Approximating a discount function using a cubic spline | 202 |
| 22.6 | Term structure class wrapping the cubic spline approximation | 203 |
| 22.7 | Calculation of the discount factor using the Cox et al. (1985) model | 205 |
| 22.8 | Class definition, Cox et al. (1985) model | 206 |
| 22.9 | Calculating a discount factor using the Vasicek functional form | 208 |
| 22.10 | Class definition, Vasicek (1977) model | 209 |
