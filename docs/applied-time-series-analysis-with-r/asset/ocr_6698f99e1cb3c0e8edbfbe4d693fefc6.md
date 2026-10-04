# ARMA Time Series Models

Theorem 3.2 provides necessary and sufficient conditions for a model of the form in Equation 3.17 to be causal and stationary. We recommend finding the roots of the characteristic equation numerically and examining the resulting factored characteristic polynomial in a factor table. This will be clarified in Section 3.2.11.

# 3.2.4 Autocorrelations of an AR(p) Model

In order to find the autocorrelations of an AR(p) process, pre-multiply each side of Equation 3.17 by $X_{i-k}$ where $k > 0$, to obtain

```
$X_{i-k}\{X_i - \phi_1 X_{i-1} - \cdots - \phi_p X_{i-p} = a_k\}$.
```

Taking expectations in Equation 3.36 yields

```
$\gamma_k = \phi_1 \gamma_{k-1} - \cdots - \phi_p \gamma_{k-p} = 0$,
```

where we have used the fact that, in the AR(I) case, $E[X_{i-k}a_i] = 0$ for $k > 0$. It follows for $k > 0$,

```
$ho_k = \phi_1 ho_{k-1} - \cdots - \phi_p ho_{k-p} = 0$.
```

Writing Equation 3.37 as

```
$ho_k = \phi_1 ho_{k-1} + \cdots + \phi_p ho_{k-p}$
```

the first $p$ equations specified in Equation 3.38 can be written as

```
$ho_1 = \phi_1 + \phi_2 ho_1 + \cdots + \phi_p ho_{p-1}$
$ho_2 = \phi_1 ho_1 + \phi_2 ho_2 + \cdots + \phi_p ho_{p-2}$
:$
$ho_p = \phi_1 ho_{p-1} + \phi_2 ho_{p-2} + \cdots + \phi_p$.
```

The equations in Equation 3.39 are called the Yule-Walker equations. When the coefficients $\phi_1, \dots, \phi_p$ are known, the Yule–Walker equations are $p$ equations that can be solved for the unknowns $ho_1, \dots, ho_p$. Note that after the first $p$ autocorrelations are found by solving the Yule–Walker equations, then $ho_k, k > p$ can be iteratively found using the relationship in Equation 3.38.

Also note that for a given set of data assumed to follow an unknown AR(p) model, the model parameters $\phi_1, \dots, \phi_p$ can be estimated by first replacing $ho_k$