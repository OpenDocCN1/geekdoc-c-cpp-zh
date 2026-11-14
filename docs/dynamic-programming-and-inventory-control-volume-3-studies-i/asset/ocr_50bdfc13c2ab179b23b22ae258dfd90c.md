# 2.4. SEVERAL PRODUCTS WITH SCARCE RESOURCE

Suppose we manage the inventory of several products with a global constraint (budget, storage possibilities). We can clearly formulate the problem: Minimize

```
\(\sum_j C_j(q_j) \quad \sum_j a_j q_j \le A ,\)
```

with, whenever each individual cost is obtained by an EOQ formula

```
\(C_j(q_j) = \frac{K_j \lambda_j}{q_j} + h_j \frac{q_j}{2}.\)
```

We can introduce a Lagrange multiplier \(\gamma\) and obtain the system

```
\(\hat{q}_j(\gamma) = \sqrt{\frac{2 K_j \lambda_j}{h_j + 2 \gamma a_j}},\)
```

and \(\gamma = \hat{\gamma} > 0\) is the unique solution of

```
\(\sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j + 2 \gamma a_j}} = A.\)
```

Note that if \(A \ge \sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j}}\), then the solution is simply that of the unconstrained problem (the constraint is not stringent). So we may assume

```
\(\sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j}} > A,\)
```

and \(\gamma\) is uniquely defined.

We note a simple case in which \(\gamma\) can be computed explicitly. Suppose we have

```
\(h_j = i \alpha_j, a_j = k \alpha_j,\)
```

where \(\alpha_j\) is the procurement price of product \(j\). This situation occurs when \(h_j\) can be interpreted as an opportunity cost and \(i\) is an interest rate, and when the constraint is on the total value of the stocks.

# Exercise 2.4. Show that

```
\(\hat{\gamma} = \frac{k}{2 A^2} \left( \sum_j \sqrt{2 K_j \lambda_j \alpha_j} \right)^2 - \frac{i}{2k}.\)
```

# 2.5. CONTINUOUS PRODUCTION OF SEVERAL PRODUCTS

We consider the situation of continuous production of several products using the same manufacturing system. Call \(r_j\) the production rate per unit of time of product \(j\). We recall that \(r_j > \lambda_j\). Since the manufacturing system is the same, we must have

```
\(\sum_j \frac{r_j}{\lambda_j} < 1.\)
```