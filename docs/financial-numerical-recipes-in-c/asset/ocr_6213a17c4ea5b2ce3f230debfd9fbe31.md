We calculate the option price using the usual roll back procedure with the continuation value

e^{-r \Delta t} (p_u f_u + p_m f_m + p_d f_d)

```
#include <vector>
#include <cmath>
using namespace std;

double option_price_put_american_trinomial( const double& S,
        const double& K,
        const double& r,
        const double& q,
        const double& sigma,
        const double& t,
        const int& steps) {
    double delta_t = t / steps;
    double Rinv = exp(-r*(delta_t));
    double sigma_sqr = pow(sigma,2);
    double u = exp(sigma*sqrt(3.0*delta_t));
    double d = 1.0/u;
    double p_u = 1.0/6.0 + sqrt(delta_t)/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);
    double p_m = 2.0/3.0;
    double p_d = 1.0/6.0 - sqrt(delta_t)/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);

    vector<double> values; // price of underlying in a tree
    vector<double> Svec;
    Svec.push_back(S);
    for (int step=1; step<=steps; ++step){
        Svec.push_back(Svec[step-1]*u); // use the fact that only the extreme values change.
        Svec.push_back(Svec[step-1]*d);
    }

    vector<double> values_next;
    for (int i=0; i<m; ++i) values_next[i] = max(0.0, K-Svec[i]); // call payoffs at maturity
    vector<double> values; // value of option
    for (int step=steps-1; step>=0; --step) {
        int m = (int(Svec[step].size();
        values = vector<double>(m); // value of option
        for (int i=0; i<m; ++i) {
            values[i] = (p_u*values_next[i+2]+p_m*values_next[i+1] + p_d*values_next[i])*Rinv;
            values[i] = max(values[i]-K-Svec[step][i]); // check for excercise
        }
        values_next=values;
    }
    return values[0];
};
```

C++ Code 18.1: Price of american put using a trinomial tree

# Example

You are given the following information about an option: S = 100, K = 100, r = 0.1, sigma = 0.25 and time to maturity is 1 year. Price an American put using a trinomial approximation with 100 steps.