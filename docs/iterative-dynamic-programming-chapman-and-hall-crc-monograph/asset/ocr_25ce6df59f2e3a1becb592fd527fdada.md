switches, giving a 5-stage control policy. To use stages of flexible length, we consider the augmented performance index

```
J = x₄(t_f) + θ(t_{fc} - t_f - s)²  (10.30)
```

where t_{fc} is the sum of the variable stage lengths, θ is a positive penalty function factor and s is a shifting term. The shifting term is chosen initially zero, and is then updated after every pass by the deviation of the calculated final time from the specified final time t_f

```
s^{q+1} = s^{q} - (t_{fc} - t_f)  (10.31)
```

where q is the pass number.

To solve this problem with IDP, we used the same parameters as in the other examples, except we took a tighter tolerance for integration with the DVERK subroutine using a local error tolerance of 10⁻⁸, rather than 10⁻⁶, and we used the penalty function factor θ as a parameter.

As can be seen in Figure 10.11, the effect of the penalty function factor is quite pronounced. Here it is very important to allow the length of the time stages to vary, and so the use of a very small value θ = 0.001 gives the optimal control policy given in Figure 10.12. The low sensitivity can be appreciated by comparing this result to the previously obtained control policy by Luus [13], which is only 0.00004% higher than the present result, yet the last two stages of the control policy are quite different. The problem of low sensitivity is considered in greater detail in Chapter 14.

![](bbox=[0.38, 0.6, 0.62, 0.84])

Figure 10.11: Effect of the penalty function factor θ on convergence for Example 4, showing the deviation from I = 1.25211 with the use of R = 25, γ = 0.95, η = 0.88, N = 1 and 30 iterations in each pass