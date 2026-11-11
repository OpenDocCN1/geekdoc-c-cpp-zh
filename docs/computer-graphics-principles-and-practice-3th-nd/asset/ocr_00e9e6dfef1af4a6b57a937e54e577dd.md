In the case of our “counting heads in a coin-flip” experiment, the expectation is

$$\mathbb{E}[X] = p(hh)X(hh) + p(ht)X(ht) + p(th)X(th) + p(tt)X(tt), \qquad (30.7)$$

$$= \frac{1}{4}\cdot 2 + \frac{1}{4}\cdot 1 + \frac{1}{4}\cdot 1 + \frac{1}{4}\cdot 0, \qquad (30.8)$$

$$= 1. \qquad (30.9)$$

If we in fact run the coin-flipping program many times, we’ll sometimes see a heads count of 0; sometimes 1; and sometimes 2. The average number of heads, over many executions of the program, will be about 1.

We can rewrite the expectation in Equation 30.7 by asking, for each possible value taken on by $X$ (i.e., 0, 1, and 2), what fraction of the items in $S$ correspond to that value. For the value 1, we have $X(ht)=1$ and $X(th)=1$, so two of the four items in $S$, in other words, half, correspond to the value 1. We then sum these fractions times the associated values, and thus compute

$$\mathbb{E}[X] = \sum_{r=0,1,2} r\cdot \Pr\{X=r\}, \qquad (30.10)$$

$$= 0\cdot\frac{1}{4} + 1\cdot\frac{1}{2} + 2\cdot\frac{1}{4} = 1. \qquad (30.11)$$

This latter form is used in many applications of probability, because it depends only on the values of $X$ and the associated probabilities, and the probability space $S$ does not appear directly. In our applications, however, this form will not appear again.

Nonetheless, the function $r \mapsto \Pr\{X=r\}$, and its generalization in the continuum case, is of substantial interest to us. Note that it’s defined on the codomain of $X$, not the domain. And for each codomain value $r$, it tells us (if we’re thinking of $X$ informally as “producing a random output”) the probability that $X$ will produce the output $r$. This function is called the **probability mass function** (or pmf) for the random variable $X$, and is denoted $p_X$.

One reason the pmf is interesting is that it can be generalized to apply to a function $Y:S\to T$, sending our probability space to any finite set $T$, not just the real numbers. For such a function, we define

$$p_Y(t)=\Pr\{Y=t\}\text{ for }t\in T. \qquad (30.12)$$

This function, $p_Y$, is a probability mass function on $T$ so that $(T,p_Y)$ becomes a probability space.

**Inline Exercise 30.3.** (a) How do we know that $p_Y$ is a probability mass function, that is, it satisfies the two requirements of non-negativity and normality? (b) If $E\subseteq T$ is an event, show that Equation 30.12 implies that the probability of the event $E$ in the space $(T,p_Y)$ is given by $\Pr_T\{E\}=\Pr_S\{Y^{-1}(E)\}$. (Here $Y^{-1}(E)$ denotes the set of all points $s\in S$ such that $Y(s)\in E$.)

We’ve now used the term “probability mass function” in two different ways: When we spoke of a probability space $(S,p)$, we called $p$ the probability mass function. But we’ve also described the pmf for a random variable $X:S\to\mathbb{R}$, or even for a function $Y:S\to T$ into an arbitrary set. We’ll now show that