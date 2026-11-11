
## 30.3.1 Discrete Probability and Its Relationship to Programs

A **discrete probability space** is a nonempty finite¹ set $S$ together with a real-valued function $p: S \to \mathbb{R}$ with two properties.

- 1. For every $s \in S$, we have $p(s) \ge 0$, and
- 2. $\sum_{s\in S} p(s) = 1$.

The first property is called non-negativity, and the second is called normality. The function $p$ is called the **probability mass function**, and $p(s)$ is the probability mass for $s$ (or, informally, the probability of $s$). The intuition is that $S$ represents a set of outcomes of some experiment, and $p(s)$ is the probability of outcome $s$. For example, $S$ might be the set of four strings hh, ht, th, tt, representing the heads-or-tails status of tossing a coin twice (see Figure 30.4). If the coin is fair, we associate probability 1/4 to each outcome.

![](img/f464cd0043eb5336aa0543fe20a0561b_853_0.png)

> **Inline Exercise 30.1:** Explain why, in a discrete probability space $(S, p)$, we have $0 \le p(s) \le 1$ for every $s \in S$. The first inequality follows from the first defining property of $p$. What about the second?

An **event** is a subset of a probability space. The **probability** of an event (see Figure 30.5) is the sum of the probability masses of the elements of the event, that is,

![](img/f464cd0043eb5336aa0543fe20a0561b_853_1.png)

$$\Pr\{E\} = \sum_{s\in E} p(s). \qquad (30.1)$$

> **Inline Exercise 30.2:** Prove that if $E_1$ and $E_2$ are events in the finite probability space $S$, and $E_1 \cap E_2 = \emptyset$, then $\Pr\{E_1 \cup E_2\} = \Pr\{E_1\} + \Pr\{E_2\}$. This generalizes, by induction, to show that for any finite set of mutually disjoint events, $\Pr\{\bigcup_{i=1}^n E_i\} = \sum_{i=1}^n \Pr\{E_i\}$. One of the axioms of probability theory is that this relation holds even for an infinite, but countable, collection of disjoint events when we’re working with continua, like $[0, 1]$ or $\mathbb{R}$, rather than a discrete probability space.

A **random variable** is a function, usually denoted by a capital letter, from a probability space to the real numbers:

$$X : S \to \mathbb{R} \qquad (30.2)$$

The terminology is both suggestive and misleading. The function $X$ is not a variable; it’s a real-valued function. It’s not random, either: $X(s)$ is a single real number for any outcome $s \in S$. On the other hand, $X$ serves as a model for something random. To give a concrete example, consider the four-element probability space described earlier. There’s a random variable $X$ defined on that space by the notion “How many heads came up?” or, more formally, “How many hs does the string contain?” To be explicit, we can define the random variable $X$ by

$$X(hh)=2 \quad X(ht)=1 \quad X(th)=1 \quad X(tt)=0. \qquad (30.3)$$

¹ Countably infinite sets such as the integers are often included in the study of discrete probability, but we’ll have no need for them, and restrict ourselves to the finite case.

In the case of our “counting heads in a coin-flip” experiment, the expectation is

$$
\mathbb{E}[X] = p(hh)X(hh) + p(ht)X(ht) + p(th)X(th) + p(tt)X(tt), \qquad (30.7)
$$

$$
= \frac{1}{4}\cdot 2 + \frac{1}{4}\cdot 1 + \frac{1}{4}\cdot 1 + \frac{1}{4}\cdot 0, \qquad (30.8)
$$

$$
= 1. \qquad (30.9)
$$

If we in fact run the coin-flipping program many times, we’ll sometimes see a heads count of 0; sometimes 1; and sometimes 2. The average number of heads, over many executions of the program, will be about 1.

We can rewrite the expectation in Equation 30.7 by asking, for each possible value taken on by $X$ (i.e., 0, 1, and 2), what fraction of the items in $S$ correspond to that value. For the value 1, we have $X(ht)=1$ and $X(th)=1$, so two of the four items in $S$, in other words, half, correspond to the value 1. We then sum these fractions times the associated values, and thus compute

$$
\mathbb{E}[X] = \sum_{r=0,1,2} r\cdot \Pr\{X=r\}, \qquad (30.10)
$$

$$
= 0\cdot\frac{1}{4} + 1\cdot\frac{1}{2} + 2\cdot\frac{1}{4} = 1. \qquad (30.11)
$$

This latter form is used in many applications of probability, because it depends only on the values of $X$ and the associated probabilities, and the probability space $S$ does not appear directly. In our applications, however, this form will not appear again.

Nonetheless, the function $r \mapsto \Pr\{X=r\}$, and its generalization in the continuum case, is of substantial interest to us. Note that it’s defined on the codomain of $X$, not the domain. And for each codomain value $r$, it tells us (if we’re thinking of $X$ informally as “producing a random output”) the probability that $X$ will produce the output $r$. This function is called the **probability mass function** (or pmf) for the random variable $X$, and is denoted $p_X$.

One reason the pmf is interesting is that it can be generalized to apply to a function $Y:S\to T$, sending our probability space to any finite set $T$, not just the real numbers. For such a function, we define

$$
p_Y(t)=\Pr\{Y=t\}\text{ for }t\in T. \qquad (30.12)
$$

This function, $p_Y$, is a probability mass function on $T$ so that $(T,p_Y)$ becomes a probability space.

> **Inline Exercise 30.3.** (a) How do we know that $p_Y$ is a probability mass function, that is, it satisfies the two requirements of non-negativity and normality? (b) If $E\subseteq T$ is an event, show that Equation 30.12 implies that the probability of the event $E$ in the space $(T,p_Y)$ is given by $\Pr_T\{E\}=\Pr_S\{Y^{-1}(E)\}$. (Here $Y^{-1}(E)$ denotes the set of all points $s\in S$ such that $Y(s)\in E$.)

We’ve now used the term “probability mass function” in two different ways: When we spoke of a probability space $(S,p)$, we called $p$ the probability mass function. But we’ve also described the pmf for a random variable $X:S\to\mathbb{R}$, or even for a function $Y:S\to T$ into an arbitrary set. We’ll now show that these uses are consistent. Consider the identity function $I:S\to S:s\mapsto s$. By Equation 30.12, we have

$$
p_I(t)=\Pr\{I=t\}\text{ for }t\in S. \qquad (30.13)
$$

For a fixed element $t\in S$, what is the event $I=t$? It’s the event

$$
\{s\in S:I(s)=t\}=\{s\in S:s=t\}=\{t\}. \qquad (30.14)
$$

The probability of this event is just the sum of the probability masses for all outcomes in the event, that is, $p(t)$. Thus, the probability mass function for the identity map is the same thing as the probability mass function $p$ for the probability space itself.

Functions like $Y$ that send a probability space to some set $T$ rather than $\mathbb{R}$ are sometimes still called random variables. In the case we’re most interested in, $Y$ will send the unit square to the unit sphere or upper hemisphere, and we’ll use the terminology “random point.” We’ll use the letter $Y$ to denote random-point functions, just as we use $X$ for all of the random variables in the chapter.

We conclude with one last bit of terminology. The function $p_Y$, whether $Y$ is a random variable or a map from $S$ to some arbitrary set $T$, is called the **distribution** of $Y$; we say that $Y$ is distributed according to $p_Y$. This suggestive terminology is useful when we’re thinking of things like student scores on a test, where it’s common to say, “The scores were distributed around a mean of 82.” In this case, the underlying probability space $S$ is the set of students, with a uniform probability distribution on $S$, and the test score is a random variable from students to $\mathbb{R}$. You’ll often see the notation $X\sim f$ to mean “X is a random variable with distribution $f$,” that is, with $p_X=f$.

## 30.3.3 Properties of Expected Value, and Related Terms

The expected value of a random variable $X$ is a constant; it’s often denoted $\bar{X}$. Note that $\bar{X}$ can also be regarded as a constant function on $S$, and hence be treated as a random variable as well.

Expectation has two properties that we’ll use frequently: $\mathbb{E}[X+Y]=\mathbb{E}[X]+\mathbb{E}[Y]$, and $\mathbb{E}[cX]=c\mathbb{E}[X]$ for any real number $c$. In short, expectation is linear.

> Expectation and variance (the latter which we’ll encounter in a moment) are higher-order functions: Their arguments are not numbers or points, but actual functions—in particular, random variables.
>
> When we write $\mathbb{E}[X+Y]$, we mean the expectation of the sum of the two random variables $X$ and $Y$, that is, the function $s\mapsto X(s)+Y(s)$. This means that when we write $X+X$, we mean the function $s\mapsto X(s)+X(s)$. If $X$ happens to correspond to a piece of code that looks like `return randb(...)`, then you cannot implement $X+X$ by `X()+X()`: The two invocations of the random number generator may produce different values!

In general, when you look at a program with `randb` in it, your analysis of the program will involve a probability space with $2^k$ elements, where $k$ is the number of times `randb` is invoked; each element will have equal probability mass. The same will be true when we look at `rand`: Any two numbers between 0 and 1 will
