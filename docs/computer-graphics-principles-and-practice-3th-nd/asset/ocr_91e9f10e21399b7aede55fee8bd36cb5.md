these uses are consistent. Consider the identity function $I:S\to S:s\mapsto s$. By Equation 30.12, we have

$p_I(t)=\Pr\{I=t\}$ for $t\in S$. (30.13)

For a fixed element $t\in S$, what is the event $I=t$? It’s the event

$\{s\in S:I(s)=t\}=\{s\in S:s=t\}=\{t\}$. (30.14)

The probability of this event is just the sum of the probability masses for all outcomes in the event, that is, $p(t)$. Thus, the probability mass function for the identity map is the same thing as the probability mass function $p$ for the probability space itself.

Functions like $Y$ that send a probability space to some set $T$ rather than $\mathbb{R}$ are sometimes still called random variables. In the case we’re most interested in, $Y$ will send the unit square to the unit sphere or upper hemisphere, and we’ll use the terminology “random point.” We’ll use the letter $Y$ to denote random-point functions, just as we use $X$ for all of the random variables in the chapter.

We conclude with one last bit of terminology. The function $p_Y$, whether $Y$ is a random variable or a map from $S$ to some arbitrary set $T$, is called the **distribution** of $Y$; we say that $Y$ is distributed according to $p_Y$. This suggestive terminology is useful when we’re thinking of things like student scores on a test, where it’s common to say, “The scores were distributed around a mean of 82.” In this case, the underlying probability space $S$ is the set of students, with a uniform probability distribution on $S$, and the test score is a random variable from students to $\mathbb{R}$. You’ll often see the notation $X\sim f$ to mean “X is a random variable with distribution $f$,” that is, with $p_X=f$.

# 30.3.3  Properties of Expected Value, and Related Terms

The expected value of a random variable $X$ is a constant; it’s often denoted $\bar{X}$. Note that $\bar{X}$ can also be regarded as a constant function on $S$, and hence be treated as a random variable as well.

Expectation has two properties that we’ll use frequently: $\mathbb{E}[X+Y]=\mathbb{E}[X]+\mathbb{E}[Y]$, and $\mathbb{E}[cX]=c\mathbb{E}[X]$ for any real number $c$. In short, expectation is linear.

> Expectation and variance (the latter which we’ll encounter in a moment) are higher-order functions: Their arguments are not numbers or points, but actual functions—in particular, random variables.
> 
> When we write $\mathbb{E}[X+Y]$, we mean the expectation of the sum of the two random variables $X$ and $Y$, that is, the function $s\mapsto X(s)+Y(s)$. This means that when we write $X+X$, we mean the function $s\mapsto X(s)+X(s)$. If $X$ happens to correspond to a piece of code that looks like `return randb(...)`, then you cannot implement $X+X$ by `X()+X()`: The two invocations of the random number generator may produce different values!

In general, when you look at a program with `randb` in it, your analysis of the program will involve a probability space with $2^k$ elements, where $k$ is the number of times `randb` is invoked; each element will have equal probability mass. The same will be true when we look at `rand`: Any two numbers between 0 and 1 will