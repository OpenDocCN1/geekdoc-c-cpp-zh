![](bbox=[0.106, 0.086, 0.926, 0.283])

Figure 8.24 The U_500(x) = 1 - e^{-x/500} function is in (a), while the U_1000(x) = 1 - e^{-x/1000} function is in (b).

In this function the parameter r, called the risk tolerance, determines the degree of risk-aversion modeled by the function. As r becomes smaller, the function models more risk-averse behavior. Figure 8.24 (a) shows U_500(x), while Figure 8.24 (b) shows U_1000(x). Notice that both functions are concave (opening downward), and the one in Figure 8.24 (b) is closer to being a straight line. The more concave the function is, the more risk averse is the behavior modeled by the function. To model risk neutrality (i.e., simply being an expected value maximizer), we would use a straight line instead of the exponential utility function, and to model risk seeking behavior we would use a convex (opening upward) function. Chapter 5 showed many examples of modeling risk-neutrality. Here, we concentrate on modeling risk-averse behavior.

Example 8.25 Suppose Sam is making the decision in Example 8.1, and Sam decides his risk tolerance r is equal to 500. Then for Sam,

```
EU(Buy NASDIP)
= EU(NASDIP)
= .25U_500($500) + .25U_500($1000) + .5U_500($2000)
= .25 (1 - e^{-500/500}) + .25 (1 - e^{-1000/500}) + .5 (1 - e^{-2000/500})
= .86504
```

EU(Leave $1000 in bank) = U_500 ($1005) = 1 - e^{-1005/500} = .86601.

So Sam decides to leave the money in the bank.

Example 8.26 Suppose Sue is less risk averse than Sam, and she decides that her risk tolerance r equals 1000. If Sue is making the decision in Chapter 5, Example 8.1, then for Sue,