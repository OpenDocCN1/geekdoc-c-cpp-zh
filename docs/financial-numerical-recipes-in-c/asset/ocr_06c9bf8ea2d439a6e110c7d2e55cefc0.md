# 5.2.2 Flat term structure.

The flat term structure overrides the yield member function of the base class.
The only piece of data this type of term structure needs is an interest rate.

```
#ifndef _TERM_STRUCTURE_CLASS_FLAT_
#define _TERM_STRUCTURE_CLASS_FLAT_

#include "term_structure_class.h"

class term_structure_class_flat : public term_structure_class {
private:
    double R_; // interest rate
public:
    term_structure_class_flat(const double& r)
    : term_structure_class_flat() {
    virtual double r(const double& t) const;
    void set_int_rate(const double& r);
    };

#endif
```

Header file 5.2: Header file for term structure class using a flat term structure

```
#include "fin_recipes.h"

term_structure_class_flat::term_structure_class_flat(const double& r) { R_ = r; };

term_structure_class_flat::~term_structure_class_flat(){};

double term_structure_class_flat::r(const double& T) const { if (T>=0) return R_; return 0; };

void term_structure_class_flat::set_int_rate(const double& r) { R_ = r; };
```

C++ Code 5.3: Implementing term structure class using a flat term structure

# Example

The term structure is flat with r = 5%. Determine the discount factors for years 1 and 2 and the forward rate between 1 and 2.

C++ program:

```
term_structure_class_flat ts(0.05);
double t1=1;
cout << "discount factor t1 = " << t1 << "," << ts.d(t1) << endl;
double t2=2;
cout << "discount factor t2 = " << t2 << "," << ts.d(t2) << endl;
cout << "spot rate t = " << t1 << " = " << ts.r(t1) << endl;
cout << "spot rate t = " << t2 << " = " << ts.r(t2) << endl;
cout << "forward rate from t1= " << t1 << " to t2= " << t2 << "," << ts.f(t1,t2) << endl;
```

Output from C++ program:

```
discount factor t1 = 1:0.951229
discount factor t2 = 2:0.904837
spot rate t = 1:0.05
spot rate t = 2:0.05
forward rate from t1= 1 to t2= 2:0.05
```