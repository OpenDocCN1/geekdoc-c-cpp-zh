
To find the value of \(a(72)\) we can either iterate the recurrence with `seq` or use `rsolve` to obtain a formula. Let’s start with iteration. (Remember to either use `restart` or open a new Worksheet to have a fresh Maple environment.) Since this is a simple recurrence, we’ll use a ‘short-cut’ procedure.

```maple
> a := n -> piecewise(n > 0, 0.75 * a(n - 1) + 100, 0);
```

$$a := n \mapsto \begin{cases}0.75\,a(n-1)+100 & 0<n\\0 & otherwise\end{cases}$$

Asking Maple for \(a(72)\) will perform the iterations and display the result.

```maple
> a(72);
```

$$399.999996$$

We could see all the iterates by using \(\operatorname{seq}(a(k), k=0..72)\). Let’s attempt to find a formula by using `rsolve`. (Remember to `restart`.)

```maple
> rsolve({a(n + 1) = 0.75 * a(n) + 100, a(0) = 0}, a(n));
```

$$400 - 400\left(\frac{3}{4}\right)^n$$

Note that, in this case, Maple returned an exact answer even though we entered decimals.

What is the long-term level of drug in the patient’s bloodstream?

```maple
> limit(400 - 400 * 0.75^n, n = infinity);
```

$$400$$

Checking iterates would show that a patient’s bloodstream would have approximately 400 mg of the drug after 24 hours.

It’s time for a plot.

```maple
> pts := [seq([n, 400 - 400 * 0.75^n], n = 0..48)]:
```

suggesting that

$$a(n)=r^n\cdot a(0)\quad\text{for }n=0,1,2,\ldots$$

Let’s check with Maple.

```maple
rsolve({a(n+1) = 1.001 * a(n), a(0) = 1000}, a(n)):
Money := unapply(%, n);
Money -> 1000 (1001/1000)^n
```

Note that Maple converts to rational numbers when using `rsolve`. Recall that `unapply` turns an expression into a function.

What is the overall trend?

```maple
Limit(Money(n), n = infinity) = limit(Money(n), n = infinity);
lim[n→∞] 1000 (1001/1000)^n = ∞
```

```maple
with(plots):
```

```maple
pointplot([seq([i, Money(i)], i = 0..12*4)], title = "Money over Time");
```

![](img/0f04050177d82aebd17d3383d7334896_62_0.png)

The graph looks like a line even though this function is obviously nonlinear.

How many years does it take for the plot to show some curvature?

Let’s look at the sequence of 4 years of values to see how *Money* grows.

```maple
Money_table := seq(eval(Money(i)), i = 0..12*4);

Money_table := 1000., 1001., 1002.001000, 1003.003001,
                1004.006004, 1005.010010, 1006.015020, 1007.021035,
                1008.028056, 1009.036084, 1010.045120, 1011.055165,
                1012.066220, 1013.078287, 1014.091365, 1015.105456,
                1016.120562, 1017.136682, 1018.153819, 1019.171973,
                1020.191145, 1021.211336, 1022.232547, 1023.254780,
                1024.278035, 1025.302313, 1026.327615, 1027.353943,
                1028.381297, 1029.409678, 1030.439088, 1031.469527,
                1032.500996, 1033.533497, 1034.567031, 1035.601598,
                1036.637199, 1037.673836, 1038.711510, 1039.750222,
                1040.789972, 1041.830762, 1042.872593, 1043.915465,
                1044.953981, 1046.004340, 1047.050345, 1048.097395,
                1049.145492
```

Can the account ever reach $10,000? We can determine that it will take about 192 years to reach $10,000.

```maple
> months := fsolve(10000 = Money(n), n);

                         months := 2303.736194

> years := months/12;

                          years := 191.9780162
```

Since \(Money(n)\) goes to infinity as \(n\) grows, the account continues to grow as long as there are no withdrawals.

## Example 2.5. A Simple Mortgage

Five years ago, your parents purchased a home by financing $150,000 over 20 years with an interest rate of 4% APR. Their monthly payments are $908.97. They have made 60 payments and wish to know what they actually owe on the house at this time. They can use this information to decide whether or not to refinance their house at a lower interest rate of 3.25% APR for the next 15 years or 3.5% APR for 20 years.

The change in the amount owed each period increases by the amount of the interest and decreases by the amount of the payment.

### General Problem

Build and use a model that relates the time to the amount owed on a mortgage for a home.

### Assumptions

- Initial interest was 4% APR.
- The monthly interest rate is 4%/12 = 0.33%.
- Payments are made on time each month.
- The current rates for refinancing are 3.25% for 15 years and 3.50% for 20 years.

### Variables

Let \(b(n)\) = amount owed on the home after \(n\) months.

### Flow Diagram

We diagram the flow in Figure 2.6.

![](img/0f04050177d82aebd17d3383d7334896_64_0.png)

FIGURE 2.6: Flow Diagram for Amount Owed on Mortgage

### Model Construction

\[
\textit{future} = \textit{present} + \textit{change}
\]
\[
b(n+1)=b(n)+(0.04/12\cdot b(n))-908.97 \quad\text{and}\quad b(0)=150000
\]
\[
=(1+0.04/12)\cdot b(n)-908.97 \quad\text{and}\quad b(0)=150000
\]

### Model Solution

Use `rsolve` to find a formula for \(b(n)\). Since Maple converts to rational numbers for `rsolve`, we’ll embed an `evalf` to return to decimals.

```maple
rsolve({b(n+1) = (1 + 0.04/12) * b(n) - 908.97, b(0) = 150000}, b(n));
b := unapply(evalf(%), n);
    b := n ↦ -122691.0273 * 1.003333333^n + 272691.0273
```

First, a reasonableness check.

```maple
b(12 * 20);

0.1695
```

The last payment leaves $0.17 to pay; this is due to round-off error in the computations as 0.04/12 is a repeating decimal value.

Let’s plot the DDS over the entire 20 years (240 months). Note the graph shows that the balance essentially reaches 0 in 240 months.

```maple
with(plots):
MCpts := [seq([i, b(i)], i = 0..240)]:
pointplot(MCpts, title = "Mortgage Balance");
```

![](img/0f04050177d82aebd17d3383d7334896_65_0.png)

Now let’s make a table of the mortgage balance up to month 60.

```maple
Mortgage_table := seq(b(i), i = 0..60);

Mortgage_table := 150000.0000, 149591.0299, 149180.6967, 148768.9957,
                  148355.9222, 147941.4719, 147525.6401, 147108.4222, 146689.8135,
                  146269.8095, 145848.4056, 145425.5968, 145001.3787, 144575.7466,
                  144148.6957, 143720.2214, 143290.3187, 142858.9831, 142426.2096,
                  141991.9936, 141556.3303, 141119.2146, 140680.6419, 140240.6074,
                  139799.1061, 139356.1329, 138911.6833, 138463.7522, 138018.3347,
                  137569.4258, 137119.0206, 136667.1138, 136213.7009, 135758.7764,
                  135302.3357, 134844.3734, 134384.8846, 133923.8641, 133461.3071,
                  132997.2080, 132531.5619, 132064.3638, 131595.6083, 131125.2903,
                  130653.4045, 130179.9458, 129704.9090, 129228.2886, 128750.0796,
                  128270.2764, 127788.8740, 127305.8668, 126821.2496, 126335.0171,
                  125847.1639, 125357.6843, 124866.5733, 124373.8251, 123879.4345,
                  123383.3959, 122885.7038
```

From the table, we see the balance on the mortgage is \(b(60) = 122885.7038\). After paying for 60 months, your parents still owe $122,885.70 of the original $150,000. They have paid a total of $54,538.20, but only $27,114.30 went towards the principal, the rest, $27,423.90, was interest. If the family continues with this loan, they will make 240 payments of $908.97 for a total of $218,152.80. They would pay a total of $68,152.80 in interest. They’ve already paid $27,423.90 in interest, so they would pay an additional $40,728.90 in interest. Should they refinance?

The alternatives for refinancing were 3.25% for 15 years or 3.50% for 20 years. Assuming no additional costs for refinancing, only securing a new mortgage for what they currently owe, $122,885.70, what is the best choice?

You will be asked to solve this problem in the exercise set.

## Exercises

Iterate and graph the following DDSs. Explain their long-term behavior. For each DDS, find a realistic scenario that it might explain/model.

1. \(a(n+1)=0.5a(n)+0.1,\quad a(0)=0.1\)
2. \(a(n+1)=0.5a(n)+0.1,\quad a(0)=0.2\)
3. \(a(n+1)=0.5a(n)+0.1,\quad a(0)=0.3\)
4. \(a(n+1)=1.01a(n)-1000,\quad a(0)=90000\)
5. \(a(n+1)=1.01a(n)-1000,\quad a(0)=100000\)
6. \(a(n+1)=1.01a(n)-1000,\quad a(0)=110000\)
7. \(a(n+1)=-1.3a(n)+20,\quad a(0)=9\)
8. \(a(n+1)=-4a(n)+50,\quad a(0)=9\)
9. \(a(n+1)=0.1a(n)+1000,\quad a(0)=9\)
10. \(a(n+1)=0.9987a(n)+0.335,\quad a(0)=72\)
11. Consider the mortgage problem in Example 2.5 (pag. 49). Determine what the cost of each refinancing alternative is compared to the current mortgage. Make a recommendation to your parents.

## 2.4 Equilibrium Values and Long-Term Behavior

### Equilibrium Values

Recall our original paradigm

> *Future = Present + Change.*

When the DDS stops changing, *change* equals zero, and so *future* equals *present*, and remains there. A value for which *change* equals 0, if any exist,
