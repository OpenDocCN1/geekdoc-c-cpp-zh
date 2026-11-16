Example Parameters r = 0.05, a = -0.1, b = 0.1, \sigma = 0.1 Use the Vasicek term structure model. Find short rate and discount factor for t = 1, and forward rate between years 1 and 2.

```
C++ program:
cout << "Example term structure calculation using the Vasicek term structure model"
<< endl;
double r=0.05; double a=-0.1; double b=0.1; double sigma=0.1;
cout << " direct calculation, discount factor (t=1): " #
<< term_structure::discount_factor((1, r, a, b, sigma) << endl;
term_structure::class vasicek vc(r,a,b,sigma);
cout << " using a term structure class " << endl;
cout << " yield (r) = " << vc.r(1) << endl;
cout << " discount factor (t=1) = " << vc.d(1) << endl;
cout << " forward rate (t1=1, t2=2 ) = " << vc.f(1,2) << endl;
Output from C++ program:
Example term structure calculation using the Vasicek term structure model
direct calculation, discount factor (t=1): 0.955408
using a term structure class
yield (t=1) = 0.0456168
discount factor (t=1) = 0.955408
forward rate (t1=1, t2=2) = 0.0281476
```

# 22.6 Readings

The methods in this chapter I first studied in my dissertation at Carnegie Mellon University in 1992, which lead to the paper published as Green and Ødegaard (1997). A textbook treatment of estimation and fitting of term structure models can be found in (Martinelli, Priaulet, and Priaulet, 2003, Ch 4)