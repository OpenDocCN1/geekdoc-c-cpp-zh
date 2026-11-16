```
double option_price_american_put_approximated_bjerksund_stensland( const double& S,
    const double& X,
    const double& r,
    const double& q,
    const double& sigma,
    const double& T );
```

////////////////////////////////// path dependent and other exotic options ////////////////////////////////

```
double option_price_call_bermudan_binomial( const double& S, const double& K, const double& r,
    const double& q, const double& sigma, const double& time,
    const vector<double>& potential_exercise_times,
    const int& steps );
```

```
double option_price_put_bermudan_binomial( const double& S, const double& K, const double& r,
    const double& q, const double& sigma, const double& time,
    const vector<double>& potential_exercise_times,
    const int& steps );
```

```
double option_price_european_lookback_call( const double& S, const double& Smin, const double& r,
    const double& q, const double& sigma, const double& time );
```

```
double option_price_european_lookback_put( const double& S, const double& Smin, const double& r,
    const double& q, const double& sigma, const double& time );
```

```
double
option_price_asian_geometric_average_price_call( const double& S, const double& K, const double& r,
    const double& q, const double& sigma, const double& time );
```

```
vector<double> simulate_lognormally_distributed_sequence( const double& S, const double& r,
    const double& sigma, const double& time, const int& no_steps );
```

```
double
derivative_price_simulate_european_option_generic( const double& S, const double& K, const double& r,
    const double& sigma, const double& time,
    double payoff( const vector<double>& S,
    const double& K ),
    const int& no_steps, const int& no_sims );
```

```
double
derivative_price_simulate_european_option_generic_with_control_variate( const double& S, const double& K,
    const double& r, const double& sigma,
    const double& time,
    double payoff( const vector<double>& S,
    const double& K ),
    const int& nsteps, const int& nosims );
```

////////////////////////////////

// payoffs of various options, to be used as function arguments in above simulations

```
double payoff_arithmetic_average_call( const vector<double>& prices, const double& K );
double payoff_geometric_average_call( const vector<double>& prices, const double& K );
double payoff_lookback_call( const vector<double>& prices, const double& unused_variable );
double payoff_lookback_put( const vector<double>& prices, const double& unused_variable );
```

////////////////////////////////

// generic binomial trees

```
double option_price_generic_binomial( const double& S, const double& K,
    double generic_payoff( const double& S, const double& K ),
    const double& r, const double& sigma, const double& t, const int& steps );
```

```
double payoff_binary_call( const double& S, const double& K );
double payoff_binary_put( const double& S, const double& K );
```