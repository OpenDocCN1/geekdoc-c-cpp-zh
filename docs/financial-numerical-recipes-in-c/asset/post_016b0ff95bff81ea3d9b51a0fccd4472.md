
## Chapter 25

## Building term structure trees using the Ho and Lee (1986) approach

### 25.1 Intro

In this section we build interest rate trees following the original paper of Ho and Lee (1986). We will follow the analysis in the paper, and use it to illustrate how you can build trees of more complex term structures than the simple binomial trees of the interest rate. The selling point of the original paper was that one could fit an initial term structure and then specify an evolution of the term structure consistent with this initial term structure.

### 25.2 Building trees of term structures

### 25.3 Ho Lee term structure class

```cpp
#include "fin_recipes.h"

class term_structure_class_ho_lee : public term_structure_class {
private:
    term_structure_class* initial_term;
    int n;
    int i;
    double delta;
    double pi;
public:
    term_structure_class_ho_lee(term_structure_class* fitted_term,
                                const int& n,
                                const int& i,
                                const double& delta,
                                const double& pi);
    double d(const double& T) const;
};

vector< vector<term_structure_class_ho_lee > >
term_structure_class_ho_lee::build_term_structure_tree(term_structure_class* initial,
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

### Header file 25.1: Term structure class for Ho-Lee

```cpp
#include "fin_recipes.h"

term_structure_class_ho_lee::term_structure_class_ho_lee(term_structure_class* fitted_term,
                                                         const int& n,
                                                         const int& i,
                                                         const double& delta,
                                                         const double& pi){
    initial_term = fitted_term;
    n = n;
    i = i;
    delta = delta;
    pi = pi;
};
```

### C++ Code 25.1: Term structure class for Ho-Lee

```cpp
#include "fin_recipes.h"

//#include "term_structure_class_ho_lee.h"

inline double hT(const double& T, const double& delta, const double& pi){
    return (1.0/pi*((1-pi)*pow(delta,T)));
};

double term_structure_class_ho_lee::d(const double& T) const{
    double d = initial_term->d(T) / initial_term->d(n);
    for (int j = 1; j <= n; ++j){
        d *= hT(T, delta, pi) / hT(n - j, delta, pi);
    };
    d *= hT(T, delta, pi) * pow(delta, T * (n - i));
    return d;
};
```

### C++ Code 25.2: Term structure class for Ho-Lee, calculation of discount function

```cpp
#include "fin_recipes.h"

vector< vector<term_structure_class_ho_lee> >
term_structure_class_ho_lee::build_term_structure_tree(term_structure_class* initial,
    const int& no_steps,
    const double& delta,
    const double& pi)
{
    vector< vector<term_structure_class_ho_lee> > hl_tree;
    for (int t = 0; t <= 5; ++t){
        hl_tree.push_back(vector<term_structure_class_ho_lee>());
        for (int j = 0; j <= t; ++j){
            term_structure_class_ho_lee hl(initial, t, j, delta, pi);
            hl_tree[t].push_back(hl);
        };
    };
    return hl_tree;
}
```

### C++ Code 25.3: Building a term structure tree

### 25.4 Pricing things

We now have access to what we need to do pricing through the recursive relationship

C(n,i) = [\pi C(n+1, i+1) + (1-\pi) C(n+1, i)] P_i^{(n)}(1)

where C(n,i) is the value of a security at time n at node i.

What we are pricing are typically state and time-contingent claims to cash flows. Let us illustrate pricing of an (European) call option on some underlying bond. Suppose this bond is risk free. Its cash flows at each future date does not depend on the state, but the timing of cash flows changes as you move in the tree. It is therefore necessary to some way figure out at date t: What are the future cash flows when you want to price the underlying bond at that date. We build a small class that contains this information, and use it, together with the term structures in the individual nodes, to find the bond price at each node. The value of the bond at the different nodes change because the term structure you use for discounting is changing. This bond price is then used to find the option value at each node.

```cpp
#include "fin_recipes.h"

class time_contingent_cash_flows {
public:
    vector<double> times;
    vector<double> cash_flows;
    time_contingent_cash_flows(const vector<double>& in_times, const vector<double>& in_cflows) {
        times = in_times;
        cash_flows = in_cflows;
    };
    int no_cflows() { return (int(times.size())); };
};

vector<time_contingent_cash_flows>
build_time_series_of_bond_time_contingent_cash_flows(const vector<double>& initial_times,
    const vector<double>& initial_cflows) {
    vector<time_contingent_cash_flows> vec_cf;
    vector<double> times = initial_times;
    vector<double> cflows = initial_cflows;
    while (times.size() > 0) {
        vec_cf.push_back(time_contingent_cash_flows(times, cflows));
        vector<double> tmp_times;
        vector<double> tmp_cflows;
        for (int i = 0; i < times.size(); ++i) {
            if (times[i] - 1.0 > 0.0) {
                tmp_times.push_back(times[i] - 1);
                tmp_cflows.push_back(cflows[i]);
            };
        };
        times = tmp_times;
        cflows = tmp_cflows;
    };
    return vec_cf;
};

double price_european_call_option_on_bond_using_ho_lee(term_structure_class* initial, const double& delta, const double& pi,
    const vector<double>& underlying_bond_cflow_times,
    const vector<double>& underlying_bond_cflows,
    const double& K, const double& time_to_maturity) {

    int T = int(time_to_maturity + 0.0001);
    vector< vector< term_structure_class* > > hl_tree
        = term_structure_class_ho_lee::build_term_structure_tree(initial, T + 1, delta, pi);
    vector<time_contingent_cash_flows> vec_cf
        = build_time_series_of_bond_time_contingent_cash_flows(underlying_bond_cflow_times, underlying_bond_cflows);

    vector<double> values(T + 1);
    for (int i = 0; i < T + 1; ++i) {
        values[i] = max(0.0, bonds.price(vec_cf[T + 1].times, vec_cf[T + 1].cash_flows, hl_tree[T + 1][i]) - K);
    };
    for (int t = T; t >= 0; --t) {
        vector<double> values_this(t + 1);
        for (int i = 0; i < t + 1; ++i)
            values_this[i] = (pi * values[i + 1] + (1.0 - pi) * values[i]) * hl_tree[t][i].d(1);
        values = values_this;
    };
    return values[0];
};
```

### C++ Code 25.4: Pricing of European call option on straight bond using Ho-Lee

### Example

You are pricing options on a 5 year zero coupon risk free bond. The options are European calls with a time to maturity of 3 years.

You will price the options using a Ho-Lee approach with parameters \(\pi = 0.5\) and \(\delta = 0.98\).

Price the option using two different assumptions about the current term structure:

- 1. The term structure is flat with an interest rate of 10% (continuously compounded).
- 2. The current term structure has been estimated using a Nelson Siegel parameterization with parameters \(\beta_0 = 0.09\), \(\beta_1 = 0.01\), \(\beta_2 = 0.01\) and \(\lambda = 5.0\).

C++ program:
```cpp
double delta = 0.98;
double pi = 0.5;
double r = 0.1;
term_structure_class* initial = new term_structure_class_flat(r);
vector<double> times;
times.push_back(5.0);
vector<double> cflows;
cflows.push_back(100);
double K = 100;
double B = 100;
int no_steps = 3;
cout << " Flat term structure " << endl;
cout << c << endl;
cout << c << endl;
delete (initial);
double beta0 = 0.09;
double beta1 = 0.01;
double beta2 = 0.01;
double lambda = 5.0;
initial = new term_structure_class_nelson_siegel(beta0, beta1, beta2, lambda);
cout << " Nelson Siegel term structure " << endl;
cout << c << endl;
cout << c << endl;
```
Output from C++ program:
Flat term structure
c = 4.64323
Nelson Siegel term structure
c = 6.3338

### Exercise 25.1.

What changes do you need to make to C++ 25.4 to price an American call option instead of an European call?

### Exercise 25.2.

If you for example want to price a bond, you need to keep track of intermediate payments of coupon. Implement such a procedure. To see that it is correct use it to price a (straight) bond and then compare the value calculated in the tree with the value using the current term structure. Then modify the code to build in a callable bond feature. What additional information must be kept track of?

### Exercise 25.3.

In the Ho and Lee (1986) paper there is a typo in equation (22). Can you see what it is?

### 25.5 References

The discussion in this chapter follows closely the original paper Ho and Lee (1986)
