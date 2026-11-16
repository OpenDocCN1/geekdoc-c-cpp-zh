where

$d_1 = \frac{\ln(\frac{V}{F}) + (r + \frac{1}{2}\sigma)(T-t)}{\sigma\sqrt{T-t}}$

Note on interpretation: The spread between risky and risk free debt determined solely by the price of the put option.

# Example

The current value of the firm V = 100. The firm has issued one bond with face value 90, which is due to be paid one year from now. The risk free interest rate is 5% and the volatility of the firms value is 25%. Determine the value of the debt.

```
C++ program:
cout << " Credit Risk Calculation " << endl;
double V=100, double F=90, double r=0.05, double T=1; double sigma=0.25;
double p = option_price.put_black_scholes(V,F,r,sigma,T);
cout << " Debt value = " << exp(-r*T)*F - p << endl;
------------------------------------------------------------
Output from C++ program:
Credit Risk Calculation
Debt value = 81.8592
```

# 21.2 Issues in implementation

+   - Firm value and firm volatility is unobservable.
+   - The model assumes a simple debt structure, most debt structures tend to be more complex.