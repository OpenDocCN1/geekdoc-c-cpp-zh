# Example

We are considering an investment with the following cash flows at dates 0, 1 and 2:

$C_0 = -100, C_1 = 10, C_2 = 110$

+   1. The current interest rate (with discrete, annual compounding) is 5%. Determine the present value of the cash flows.

+   2. Find the internal rate of return of this sequence of cash flows.

```
Matlab program:
C=[-100 10 110]
t=[0 1 2]
r = 0.05
d=(1/(1+r)).^t
NPV=C*d'
IRR = irr(C)
Output from Matlab program:
C =
 -100  10  110
t =
 0  1  2
r =
 0  0.050000
d =
 1.00000  0.95238  0.90703
NPV =  9.2971
IRR =  0.100000
```

```
C++ program:
vector<double> cflows; cflows.push_back(-100.0); cflows.push_back(10.0); cflows.push_back(110.0);
vector<double> times; times.push_back(0); times.push_back(1); times.push_back(2);
double r=0.05;
cout << " present value, 5 percent discretely compounded interest = " ;
cout << cash_flow_pv_discrete(times, cflows, r) << endl;
cout << " internal rate of return, discrete compounding = ";
cout << cash_flow_irr_discrete(times, cflows) << endl;
Output from C++ program:
present value, 5 percent discretely compounded interest = 9.29705
internal rate of return, discrete compounding = 0.1
```