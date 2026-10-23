The output from this program is:

```
(1,2,2)
(-1,-2,-2)
(0,0,0)
(1.79769e+308,1.79769e+308,1.79769e+308)
(2.71,3.14,3.14286)
(-3.14,-3.14,-3.1415)
(5.2,3.3,2.3)
(-5.2,-3.3,-2.3)
```

The code in this section is a template or exemplar when dealing with more extended examples. See Exercise 2.

# 31.2.2 Boost Parameter and Option Data

We continue our discussion of Boost Parameter with an application to create the parameters needed by the Monte Carlo method for one-factor option pricing applications. We define these parameters as keywords:

```
#include <boost/parameter.hpp>

namespace OptionParams
{
    BOOST_PARAMETER_KEYWORD(Tag, strike)
    BOOST_PARAMETER_KEYWORD(Tag, expiration)
    BOOST_PARAMETER_KEYWORD(Tag, interestRate)
    BOOST_PARAMETER_KEYWORD(Tag, volatility)
    BOOST_PARAMETER_KEYWORD(Tag, dividend)
    BOOST_PARAMETER_KEYWORD(Tag, optionType)
}
```

We encapsulate option data in a struct that has appropriate constructors:

```
// Encapsulate all data in one place
struct OptionData
{ // Option data + behaviour
    double K;
    double T;
    double r;
    double sig;
    // Extra data
    double D;      // dividend
    int type;      // 1 == call, -1 == put
```