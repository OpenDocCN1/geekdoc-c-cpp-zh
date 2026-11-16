```
```cpp
#include "fin_recipes.h"

class term_structure_class_ho_lee : public term_structure_class {
private:
    term_structure_class* initial_term.;
    int n.;
    int i.;
    double delta.;
    double pi.;
public:
    term_structure_class_ho_lee(term_structure_class* fitted_term,
                                const int& n,
                                const int& i,
                                const double& lambda,
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
```

# Header file 25.1: Term structure class for Ho-Lee

```
```cpp
#include "fin_recipes.h"

term_structure_class_ho_lee::term_structure_class_ho_lee(term_structure_class* fitted_term,
                                                         const int& n,
                                                         const int& i,
                                                         const double& delta,
                                                         const double& pi){
    initial_term.=fitted_term;
    n.=n;
    i.=i;
    delta.=delta;
    pi.=pi;
};
```
```

# C++ Code 25.1: Term structure class for Ho-Lee