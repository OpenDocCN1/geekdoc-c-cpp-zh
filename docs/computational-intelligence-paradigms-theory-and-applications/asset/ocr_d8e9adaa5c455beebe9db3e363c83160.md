**TABLE 13.1: Strings and Fitness Value**

| S No | String | Fitness |
|---|---|---|
| 1 | 10001 | 20 |
| 2 | 11100 | 10 |
| 3 | 00011 | 5 |
| 4 | 01110 | 15 |

# ### Solution:

*Schema Theorem:*

$$E(n(S,t+1)) \ge \frac{\hat{u}(S,t)}{\bar{f}(t)} n(S,t)\left(1-p_c\frac{d(S)}{m-1}\right)\left((1-p_m)^{o(S)}\right)$$

$$\hat{u}(S,t)=\frac{20+10}{2}=15$$

$$\bar{f}(t)=\frac{20+10+5+15}{4}=12.5$$

The number of strings covered by the given schema in generation 1 is:

$$E(n(S,t+1))=2*\frac{15}{12.5}*\left[1-1.0*\frac{0}{4}-0.01*1\right]=2*1.2*(1-0.0-0.01)=2.376$$

# ### Illustration 3:

Suppose a schema S which, when present in a particular string, causes the string to have a fitness 25% greater than the average fitness of the current population. If the destruction probabilities for this schema under mutation and crossover are negligible, and if a single representation of the schema is present at generation 0, determine when the schema H will overtake the populations of size n = 20; 50; 100; 200.

# ### Solution:

$$\hat{u}(S,t) \ge \hat{u}(S,t-1)*\frac{\bar{u}(S,t-1)}{\bar{f}(t-1)}*1$$

$$\hat{u}(S,t-2)*1.25*1.25$$

$$M$$

$$\hat{u}(S,0)*(1.25)^t$$

$$(1.25)^t$$