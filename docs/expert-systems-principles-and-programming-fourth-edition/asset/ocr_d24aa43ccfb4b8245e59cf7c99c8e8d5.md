```
S(x; α, β, γ) = \begin{cases} 0 & \text{for } x \le \alpha \\ 2 \left(\frac{x - \alpha}{\gamma - \alpha}\right)^2 & \text{for } \alpha \le x \le \beta \\ 1 - 2 \left(\frac{x - \gamma}{\gamma - \alpha}\right)^2 & \text{for } \beta \le x \le \gamma \\ 1 & \text{for } x \ge \gamma \end{cases}
```

A plot of the S-function is shown in Figure 5.9.

# Figure 5.9 The S-Function

![](bbox=[0.22, 0.33, 0.92, 0.5])

The S-function can be a valuable tool in defining fuzzy functions such as the word tall. Rather that maintaining a table of data defining the membership function, all the data may be compactly represented by a formula. In this definition, α, β, and γ are parameters that may be adjusted to fit the desired membership data. Depending on the given membership data, it may be possible to give an exact fit for some values of α, β, and γ, or the fit may be only approximate. Of course, the membership function may simply be defined as an S-function with no reference to any tabular data. Other functions, such as triangular ones, may also be defined depending on the application.

The S-function is flat at a value of 0 for x ≤ α and at 1 for x ≥ γ. In between α and γ the S-function is a quadratic function of x. As you can see from Figure 5.9, the β parameter corresponds to the crossover point of 0.5 and is (α + γ) / 2. For the TALL membership function of Figure 5.8, the S-function is the following: