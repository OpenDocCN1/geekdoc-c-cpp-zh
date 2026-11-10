Therefore

$$\begin{aligned} n &\le (1.25)^t \\ t &\ge \log_{1.25}(n) \\ &\ge \frac{\log(n)}{\log(1.25)} \end{aligned}$$

The schema will overtake the populations when,

+   $$\begin{aligned} n &= 20 \Rightarrow t \ge 14 \\ n &= 50 \Rightarrow t \ge 18 \\ n &= 100 \Rightarrow t \ge 21 \\ n &= 200 \Rightarrow t \ge 24 \end{aligned}$$

# Illustration 4:

Suppose a schema $S$ which, when present in a particular string, causes the string to have fitness 10% less than the average fitness of the current population. Suppose that the schema theorem is equality instead of an inequality and that the destruction probabilities for this schema under mutation and crossover can be ignored. If representatives of the schema are present in 60% of the population at generation 0, calculate when schema $H$ will disappear from the population of size $n = 20; 50; 100; 200$.

Solution:

$$\begin{aligned} \hat{S}, t &= \hat{u}(S,0) * (0.9)^t \\ &= 0.6 * n * (0.9)^t \\ &\ge \frac{1}{2} * n * (0.9)^t \\ \frac{1}{1.2 * n} &> (0.9)^t \\ t &> \log_{0.9}\left(\frac{1}{1.2 * n}\right) \end{aligned}$$

The given schema disappears when,

+   $$\begin{aligned} n &= 20 \Rightarrow t \ge 31 \\ n &= 50 \Rightarrow t \ge 39 \\ n &= 100 \Rightarrow t \ge 46 \\ n &= 200 \Rightarrow t \ge 53 \end{aligned}$$