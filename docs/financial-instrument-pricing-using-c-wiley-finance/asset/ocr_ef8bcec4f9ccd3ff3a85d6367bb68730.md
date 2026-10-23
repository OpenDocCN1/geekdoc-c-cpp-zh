# ## 12.9 TRINOMIAL MODEL OF THE ASSET PRICE

In Chapter 11 we introduced the binomial method and we used it to price European and American options. In general, the method is not as robust as other numerical methods. We now introduce the *trinomial method* that generalises the binomial method. The trinomial method is also easier to work with because the corresponding grid is more regular and flexible than the corresponding binomial grid. In general, we can achieve the same accuracy using the trinomial method compared to the binomial method but needing fewer mesh points.

We now discuss option pricing based on the well-known methods and pseudocode presented in Clewlow and Strickland (1998) in which the authors transform the SDE for risk-neutral geometric Brownian motion:

```
$$dS=(r-D)Sdt+\sigma SdW$$ \tag{12.26}
```

where:

+   - $r$ = risk-free interest rate
+   - $D$ = continuous dividend yield
+   - $S$ = asset price
+   - $\sigma$ = volatility
+   - $dW$ = Wiener process
+   - $dt$ = small interval of time (mesh size).

Equation (12.26) is the starting point for more advanced models. Our interest in this chapter is in showing how to use the trinomial method to calculate the price of an option. It is convenient to use a logarithmic variable $x=\log(S)$ in which case, by using Ito’s lemma the SDE in equation (12.26) becomes:

```
$$dx=\nu dt+\sigma dW \quad \text{where} \quad \nu=r-\frac{1}{2}\sigma^2.$$ \tag{12.27}
```

Then, the stochastic variable $x$ can move up, down or retain the same value in a small interval of time $\Delta t$. Each movement has an associated probability having the values:

```
$$p_u=\frac{1}{2}(\alpha+\beta)$$

$$p_m=1-\alpha$$

$$p_d=\frac{1}{2}(\alpha-\beta)$$ \tag{12.28}
```

where:

```
$$\alpha=\frac{\sigma^2\Delta t+\nu^2\Delta t^2}{\Delta x^2}, \quad \beta=\frac{\nu\Delta t}{\Delta x}.$$
```

The probabilities add up to 1:

```
$$p_u+p_m+p_d=1.$$
```