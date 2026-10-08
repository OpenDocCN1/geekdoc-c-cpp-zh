factors that influence the dependent variables $Y_i$ other than the independent variable $X_i$. It is a necessary condition that the independent variables $X_i$ are linearly independent i.e. it is not possible to express any independent variable as a linear combination of the others. Alternatively, this implies that the regression model has no multi-collinearity i.e. there is no strong correlation between two or more independent variables. In addition, the dependent variables $Y_i$ should also be approximately normally distributed.
The intercept $(a)$ can be calculated from the following rearrangement of the regression equation for $X$ and $Y:

```
$a = ar{y} - bar{x}$
```

and the slope $(b)$ from:

```
$b = \frac{\sum_{i=1}^{n}(X_i - \bar{x})(Y_i - \bar{y})}{\sum_{i=1}^{n}(X_i - \bar{x})^2}$
```

where $ar{x}$ and $ar{y}$ are the mean values of $X_i$ and $Y_i$. Source 4.10 shows the Intercept() and Slope() member functions and method implementations from the newly LinReg class.

# SOURCE 4.10: THE Intercept() AND Slope()member FUNCTIONS AND METHOD IMPLEMENTATIONS

```
// LinReg.h
#pragma once;

#include "Maths.h"
#include "Stats.h"
#include "Utils.h"

class LinReg{
public:
    LinReg() {}
    virtual ~LinReg() {}

    // Member function declarations
    DBL Intercept(const V2DD& v); // Intercept()
    DBL Slope(const V2DD& v); // Slope())
private:
    // Member variable declarations
    Stats m_stats; // An instance of the Stats class
```