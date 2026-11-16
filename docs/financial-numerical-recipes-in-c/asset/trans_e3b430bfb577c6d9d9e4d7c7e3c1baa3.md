

const vector<double>& dividend_yields);

double option_price_put_american_proportional_dividends_binomial(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_step, const vector<double>& dividend_times, const vector<double>& dividend_yields);

double option_price_delta_american_call_binomial(const double& S, const double& K, const double& r, const double& sigma, const double& t, const int& no_steps);

double option_price_delta_american_put_binomial(const double& S, const double& K, const double& r, const double& sigma, const double& t, const int& no_steps);

void option_price_partials_american_call_binomial(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_steps, double& delta, double& gamma, double& theta, double& vega, double& rho);

void option_price_partials_american_put_binomial(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_steps, double& delta, double& gamma, double& theta, double& vega, double& rho);

double futures_option_price_call_american_binomial(const double& F, const double& K, const double& r, const double& sigma, const double& time, const int& no_steps);

double futures_option_price_put_american_binomial(const double& F, const double& K, const double& r, const double& sigma, const double& time, const int& no_steps);

double currency_option_price_call_american_binomial(const double& S, const double& K, const double& r, const double& r_f, const double& sigma, const double& t, const int& n);

double currency_option_price_put_american_binomial(const double& S, const double& K, const double& r, const double& r_f, const double& sigma, const double& t, const int& n);

### 有限差分法

double option_price_call_american_finite_diff_explicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_put_american_finite_diff_explicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_call_european_finite_diff_explicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_put_european_finite_diff_explicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_call_american_finite_diff_implicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_put_american_finite_diff_implicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_call_european_finite_diff_implicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

double option_price_put_european_finite_diff_implicit(const double& S, const double& K, const double& r, const double& sigma, const double& time, const int& no_S_steps, const int& no_t_steps);

### 模拟期权价格

- 收益仅为终端价格的函数

double option_price_call_european_simulated(const double& S, const double& K, const double& r, const double& sigma, const double& time_to_maturity, const int& no_sims);

double option_price_put_european_simulated(const double& S, const double& K, const double& r, const double& sigma, const double& time_to_maturity, const int& no_sims);

double option_price_delta_call_european_simulated(const double& S, const double& K, const double& r, const double& sigma, const double& time_to_maturity, const int& no_sims);

double option_price_delta_put_european_simulated(const double& S, const double& K, const double& r, const double& sigma, const double& time_to_maturity, const int& no_sims);

double simulate_lognormal_random_variable(const double& S, const double& r, const double& sigma, const double& time);

double derivative_price_simulate_european_option_generic(const double& S, const double& K, const double& r, const double& sigma, const double& time, double payoff(const double& S, const double& K), const int& no_sims);

double derivative_price_simulate_european_option_generic_with_control_variate(const double& S, const double& K, const double& r, const double& sigma, const double& time, double payoff(const double& S, const double& K), const int& no_sims);

double derivative_price_simulate_european_option_generic_with_antithetic_variate(const double& S, const double& K, const double& r, const double& sigma, const double& time, double payoff(const double& S, const double& K), const int& no_sims);

### 各类期权的收益函数，用作上述模拟中的函数参数

double payoff_call(const double& S, const double& K);

double payoff_put(const double& S, const double& K);

double payoff_cash_or_nothing_call(const double& S, const double& K);

double payoff_asset_or_nothing_call(const double& S, const double& K);

### 近似期权价格

double option_price_american_put_approximated_johnson(const double& S, const double& X, const double& r, const double& sigma, const double& time);

double option_price_american_call_approximated_baw(const double& S, const double& K, const double& r, const double& b, const double& sigma, const double& time);

double option_price_american_put_approximated_baw(const double& S, const double& K, const double& r, const double& b, const double& sigma, const double& time);

double option_price_american_put_approximated_geke_johnson(const double& S, const double& X, const double& r, const double& sigma, const double& time);

double option_price_american_call_approximated_bjerksund_stensland(const double& S, const double& X, const double& r, const double& q, const double& sigma, const double& time);

