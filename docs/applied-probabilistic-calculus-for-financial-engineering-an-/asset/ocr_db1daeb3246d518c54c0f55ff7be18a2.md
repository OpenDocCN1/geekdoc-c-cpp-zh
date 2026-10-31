# Description

Produces an amortization table for paying off a loan while also solving for either the number of payments, loan amount, or the payment amount. In the amortization table, the payment amount, interest paid, principal paid, and balance of the loan are given for each period. If n ends up not being a whole number, outputs for the balloon payment, drop payment, and last regular payment are provided. The total interest paid, and total amount paid is also given. It can also plot the percentage of each payment toward interest versus period.

# Usage

```
amort.table(Loan=NA, n=NA, pmt=NA, i=0.025,
    ic=1, pf=1, plot=TRUE)
```

# Arguments

+   Loan loan amount
+   n the number of payments/periods
+   pmt value of level payments
+   i nominal interest rate convertible ic times per year
+   ic interest conversion frequency per year
+   pf the payment frequency- number of payments per year
+   plot tells whether or not to plot the percentage of each payment toward interest vs.period

# Details

Effective Rate of Interest: eff.i = [1 + (i/ic)]^ic - 1
j = (1 + eff.i)^(1/pf) - 1
Loan = pmt * a_nj
Balance at the end of period t: B_t = pmt * a_{n-t}j
Interest paid at the end of period t: i_t = B_{t-1}*
Principal paid at the end of period t: p_t = pmt - i_t
Total Paid = pmt * n
Total Interest Paid = pmt * n - Loan
If n = n* + k where n* is an integer and 0 < k < 1:
Last regular payment (at period n*) = pmt * s_{k/j}
Drop payment (at period n* + 1) = Loan * (1 + j)^{n*+1} - pmt * s_{n* j}
Balloon payment (at period n*) = Loan * (1 + j)^{n*} - pmt * a_{n*j} + pmt