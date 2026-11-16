
should contain approximately the same number of samples. This is a big "if". In many practical situations, particularly when participants are self-selecting, this is not possible. This is why white students are over-represented in psychological experiments, since the participants are recruited among the student population of the university where the experiment is conducted. Another oddity about this data is that all the age ranges encompass ten years, apart from the youngest and oldest. There are of course practical reasons for this, since for the youngest age range only legal adults could take part, and at the other end of the range, it is needed to ensure there are enough participants in the oldest. These are just some examples of the care which needs to be taken when gathering data.

As well as the above, in this example the percentage of smokers varies across the age ranges:

| | 18 - 24 | 25 - 34 | 35 - 44 | 45 - 54 | 55 - 64 | 65 - 74 | 75+ |
|---|---|---|---|---|---|---|---|
| smokers | 47% | 44% | 47% | 63% | 49% | 22% | 17% |

The non-smokers are disproportionally overrepresented in the two oldest age groups which are naturally more likely to die within the next twenty years. This skews the overall mortality in favour of the smokers. When the data is aggregated into just two groups of smokers and non-smokers.

We can now estimate the mortality for smokers and non-smokers for each of the age groups. Or in other words the estimated conditional probability of death given the age group and whether they were smokers or not, p(died|Y):

| | | mortality |
|---|---|---|
| 18-24 | smokers | 3.6% |
| | non-smokers | 1.6% |
| 25-34 | smokers | 2.4% |
| | non-smokers | 3.2% |
| 35-44 | smokers | 12.8% |
| | non-smokers | 5.8% |
| 45-54 | smokers | 20.8% |
| | non-smokers | 15.4% |
| 55-64 | smokers | 44.3% |
| | non-smokers | 33.1% |
| 65-74 | smokers | 80.6% |
| | non-smokers | 78.3% |
| 75+ | smokers | 100% |
| | non-smokers | 100% |

Now the mortality reflects the health advice given. In all age groups but two, the mortality of smokers is higher. Smokers die younger on average which might in part explain their under-representation in the two oldest age groups.

Simpson's paradox is due to another variable influencing the data, but hiding. This is called the *confounding variable*. In this case, it is the ages of the women in the original study and the distribution of smokers and non-smokers within the different age groups. Whenever the distributions within a population (the women in the original study) varies for different parts of the population (the different age groups), data analysis has to be done carefully, taking these variations into account.

Another example of Simpson's paradox is the correlation between price and demand. Here the confounding variable is time. If time is not taken into account, price and demand can appear positively correlated, while in fact they are negatively correlated which becomes apparent when plotting both demand and price against time.

## 2.2 Probability Densities, Expectation, Variance and Moments

In the previous sections, the random variables were discrete. However, one of them, the age, is fundamentally a continuous variable, if it is considered as time passed since birth. It was *discretized* by considering age groups. The choice of how to discretize can influence the interpretation as well. We have already seen that no discretization at all leads to the wrong interpretation of mortality with smokers being less likely to die than non-smokers. On the other hand, the discretization shall not be too fine grained, because then the number of samples in each category becomes too small for interpretation. This is also known as *over-fitting*, where the model fits the data too exactly and does not generalize to unseen data. For example, assume that we discretized the ages so finely that in each age group there is only one woman, or possibly none. We can then either make no prediction at all for a new participant of the study, if that age group is empty, or we will make the prediction according to the mortality of that one woman in that age group, which could be completely wrong.

Discretization is one way of dealing with probabilities of a continuous real-valued variable $x$. Another way is the *probability density function* (*pdf*) $f(x)$ over $x$ which describes the distribution. Formally, it is defined by $f(x)\Delta x$ being the probability of a sample falling inside the interval $(x, x + \Delta x)$ as the interval size $\Delta x$ approaches zero. The probability density function is always non-negative. It can be viewed as taking discretization to the limit. There is a valid probability value for $x$ falling into any interval $(a, b)$ and it is given by

\(p(x \in (a, b)) = \int_a^b f(x) dx.\)

![](img/d3c00252180686426c9e63ab889b535b_34_0.png)

Figure 2.2: The normal probability density function for various values of \(\mu\) and \(\sigma\).

If \(a = -\infty\) and \(b = \infty\), that is we integrate over all possible values of \(x\), the probability has to be one.

As continuous variables can be discretized, discrete variables can be viewed as continuous. In this case, \(f(x)\) is called the *probability mass function* (*pmf*), because the probabilities for each discrete possible value of \(x\) are concentrated as point masses at these values. For all other values of \(x\) the probability is zero.

A well-known example of a probability density function is the *bell curve* of a normal distribution also known as the Gaussian distribution \(x \sim \mathcal{N}(\mu, \sigma^2)\), where \(\sim\) means 'is distributed as'. Its probability density function is given by

\[
\mathcal{N}(x|\mu, \sigma^2) = \frac{1}{\sqrt{2\pi}\sigma} \exp \left( - \frac{1}{2\sigma^2}(x-\mu)^2 \right). \quad (2.4)
\]

Its position and shape are determined by the parameters \(\mu\), called the *mean*, and \(\sigma^2\), known as the *variance*. The square root of the variance, \(\sigma\), is called the *standard deviation*. Figure 2.2 illustrates the shapes of the bell curve for various values of the mean and variance. When \(\mu = 0\) and \(\sigma = \sigma^2 = 1\), it is known as the *standard normal distribution*.

There is a common misconception that "normal" means common. Gauss introduced the naming with "normal" referring to a norm as in the method of Ordinary Least Squares discussed in Section 8.4. One technique to minimize the norm is to solve the "normal" equations and these were what Gauss in his choice of words referred to. Over the years, "normal" took on the meaning of "usual".

Normal distributions are indeed quite common. Lyon elaborates on the explanations of this in [27]. The *central limit theorem* is often quoted. It states that, if $x_1, ..., x_n$ is a sequence of *independent and identically distributed* (i.i.d.) random variables with mean 0 and variance $\sigma^2$, then the distribution of the normalized sum

$$S_n = \frac{x_1 + ... + x_n}{\sqrt{n}}$$

is close to a normal distribution for large enough $n$. As $n$ tends to infinity and $S_n \to S$, it approaches the normal distribution $\mathcal{N}(S|0, \sigma^2)$. This holds however the distribution of $x_1, ..., x_n$ appeared in the first place, as long as they are independent and identically distributed. This, however, is the crux of the whole explanation.

While some phenomena we want to describe using probability density functions might be the result of independent and identically distributed summands, many are influenced by different factors, all of which have their own distinct distributions. Take for example a person's height. There is their potential for growth determined by their genetic make-up, where also different genes play a role. This is the nature part. Next is the nurture part. Nutrition, pollution, diseases, etc. all are factors. All these are not independent and identically distributed, but height is still normally distributed.

Another explanation involves the *entropy* of the probability density $f(x)$ defined as

$$-\int_{-\infty}^{\infty} f(x) \log f(x) \, dx,$$

where $f(x) \log f(x)$ is zero, wherever $f(x) = 0$. A change of base for the logarithm results in scaling of the entropy. As long as the same base is used throughout, entropies of different distributions can be compared. Information theorists prefer to use base 2 in line with bits. Since $0 \le f(x) \le 1$, the entropy is non-negative. Entropy is often interpreted as a measure of disorder or randomness or lack of information. The larger the entropy, the more disorder, the less information. For example, if there is only one possible value for $x$ with probability 1, then $\log f(x) = 0$ there and the integrand is zero everywhere. Hence the entropy is zero. The information value is perfect, since the outcome is determined. Many physical systems strive to maximize the entropy over time. For a given mean $\mu$ and variance $\sigma^2$, $f(x) = \mathcal{N}(x|\mu, \sigma^2)$ maximizes the entropy. So this choice mirrors a natural process. Also, it is wise to choose a distribution with the least information, if nothing else is known.

To show that the normal distribution integrates to one, we consider

$$\int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi}\sigma} \exp \left( -\frac{1}{2\sigma^2} (x-\mu)^2 \right) \, dx.$$

Letting $x - \mu = \sigma y$, we have $dx = \sigma dy$. The range of integration does not change with this change of variables. Thus we arrive at

$$\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} \exp \left( -\frac{y^2}{2} \right) \, dy.$$
