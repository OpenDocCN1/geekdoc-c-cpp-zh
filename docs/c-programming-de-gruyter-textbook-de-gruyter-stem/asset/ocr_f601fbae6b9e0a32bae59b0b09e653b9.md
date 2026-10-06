# 12 1 Introduction

Therefore, if we divide $N$ by $R$, the quotient is $Q_1$ and the remainder is $X_0$. Similarly,
we have

$Q_1 = X_1 + Q_2R$

Divide $Q_1$ by $R$, the quotient is $Q_2$ and the remainder is $X_1$,

```
$Q_i = X_i + (X_{i+1} + X_{i+2}R^1 + \dots + X_{n-1}R^{n-2-i})R$
$Q_i = X_i + Q_{i+1}R$
```

Divide $Q_i$ by $R$, the quotient is $Q_{i+1}$ and the remainder is $X_i$
Continue the division until the quotient is 0. The remainders $X_0, X_1, X_2 \dots X_{n-1}$ that we get constitutes the resulting $R$-based number.
For example, we can convert the decimal value 68 into a binary number like:

| | 68 | Remainder |
|---|---|---|
| 2 | 34 | ... ... 0 low order digit |
| | 17 | ... ... 0 |
| | 8 | ... ... 1 |
| 2 | 4 | ... ... 0 |
| | 2 | 2 | ... ... 0 high order digit |
| | 1 |

so $68_{10} = 1000100_2$
To convert $68_{10}$ into an octal number, we can divide it by 8 and get the remainders:

| | 168 | Remainder |
|---|---|---|
| 8 | 21 | ... ... 0 low order digit |
| | 2 | ... ... 5 |
| | | ... ... 2 high order digit |

So $68_{10} = 104_8$

**b) Decimal fraction to $R$-based fraction**
When a decimal fraction is converted into an $R$-based number, we can multiply the decimal fraction by $R$ continuously, and the integer array we get constructs the $R$-based fraction. This method is named “multiply by $R$ and get the integers”:
 can convert a decimal fraction to the $R$-based fraction like:

```
$V = \frac{X_{-1}}{R^1} + \frac{X_{-2}}{R^2} + \frac{X_{-3}}{R^3} + \dots + \frac{X_{-m}}{R^m}$
```

Multiplying both sides of the equation by $R$, we get:

```
$V 	imes R = X_{-1} + (\frac{X_{-2}}{R^1} + \frac{X_{-3}}{R^2} + \dots + \frac{X_{-m}}{R^{m-1}}) = X_{-1} + F_1$
```