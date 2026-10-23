We now turn our attention to implementing systems (24.49) (and (24.48) commented in the code) in C++. The augmented ODE class is:

```
using value_type = double;
using vector_type = boost::numeric::ublas::vector<value_type>;
using matrix_type = boost::numeric::ublas::matrix<value_type>;

struct StiffSystem
{
    void operator()(const vector_type& x , vector_type& dxdt ,
                    value_type t)
    { // Lambert page 213

        // Non-stiff form
        /* dxdt[0] = -2.0 * x[0] + 1.0 * x[1] + (2.0*std::sin(t));
           dxdt[1] = 1.0 * x[0] - 2.0 * x[1]
             + (2.0*(std::cos(t) - std::sin(t)));*/

        // Stiff form
        dxdt[0] = -2.0 * x[0] + 1.0 * x[1] + (2.0*std::sin(t));
        dxdt[1] = 998.0 * x[0] - 999.0 * x[1]
            + (999.0*(std::cos(t) - std::sin(t)));
    }
};
```

```
struct StiffSystemJacobi
{
    void operator()(const vector_type& /* x */ , matrix_type& J ,
                    const value_type& t, vector_type& dfdt )
    {
        // Non-stiff form
        /* J(0,0) = -2.0;
        J(0,1) = 1.0;
        J(1,0) = 1.0;
        J(1,1) = -2.0;*/

        // Stiff form
        J(0,0) = -2.0;
        J(0,1) = 1.0;
        J(1,0) = 998.0;
        J(1,1) = -999.0;

        // Derivative wrt t of RHS
        // Non-stiff
        /*dfdt[0] = 2.0 * std::cos(t);
        dfdt[1] = 2.0 * (-std::sin(t) - std::cos(t));*/

        // Stiff
        dfdt[0] = 2.0 * std::cos(t);
```