```
```cpp
#include <cmath>
#include <vector>
using namespace std;
#include "normdist.h"

vector<double>
simulate_lognormally_distributed_sequence(const double& S,
    const double& r,
    const double& sigma,
    const double& time, // time to final date
    const int& no_steps){ // number of steps
    vector<double> prices(no_steps);
    double delta_t = time/no_steps;
    double R = (r-0.5*pow(sigma,2))*delta_t;
    double SD = sigma * sqrt(delta_t);
    double S_t= S; // initialize at current price
    for (int i=0; i<no_steps; ++i) {
        S_t = S_t * exp(R + SD * random_normal()));
        prices[i]=S_t;
    }
    return prices;
};
```
```

# C++ Code 16.4: Simulating a sequence of lognormally distributed variables

```
```cpp
#include <cmath>
using namespace std;
#include "fin_recipes.h"

double
derivative_price_simulate_european_option_generic(const double& S,
    const double& K,
    const double& r,
    const double& sigma,
    const double& time,
    double payoff(const vector<double>& prices, const double& X),
    const int& no_steps,
    const int& no_sims) {
    double sum_payoffs=0;
    for (int n=0; n<no_sims; n++) {
        vector<double> prices = simulate_lognormally_distributed_sequence(S,r,sigma,time,no_steps);
        sum_payoffs += payoff(prices,K);
    }
    return exp(-r*time) * (sum_payoffs/no_sims);
};
```
```

# C++ Code 16.5: Generic routine for pricing European options