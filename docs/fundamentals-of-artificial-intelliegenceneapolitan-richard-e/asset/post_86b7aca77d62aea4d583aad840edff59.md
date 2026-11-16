
Proof. Because the probability is the same regardless of the order in which the heads and tails occur, we can assume all the heads occur first. We therefore have (as before, the notation s,t on the right side of the conditioning bar means that we have seen s heads and t tails) the following:

P(D)
= P(X_{s+t} = tails|s, t-1) \cdots P(X_{s+2} = tails|s, 1)P(X_{s+1} = tails|s, 0)
P(X_s = heads|s-1, 0) \cdots P(X_2 = heads|1, 0)P(X_1 = heads)
= \frac{b+t-1}{a+b+s+t-1} \times \cdots \frac{b+1}{a+b+s+1} \times \frac{b}{a+b+s} \times
\frac{a+s-1}{a+b+s-1} \times \cdots \frac{a+1}{a+b+1} \times \frac{a}{a+b}
= \frac{(a+b-1)!}{(a+b+s+t-1)!} \times \frac{(a+s-1)!}{(a-1)!} \times \frac{(b+t-1)!}{(b-1)!}
= \frac{(m-1)!}{(m+n-1)!} \times \frac{(a+s-1)!(b+t-1)!}{(a-1)!(b-1)!}

The first equality is due to Theorem 12.1. This completes the proof. ■

Example 13.2 Suppose that, before tossing a thumbtack, we assign a = 3 and b = 5 to model the slight belief that tails is more probable than heads. We then toss the coin ten times and obtain four heads and six tails. Owing to the preceding theorem, the probability of obtaining these data D is given by

P(D) = \frac{(m-1)!}{(m+n-1)!} \times \frac{(a+s-1)!(b+t-1)!}{(a-1)!(b-1)!}
= \frac{(8-1)!}{(8+10-1)!} \times \frac{(3+4-1)!(5+6-1)!}{(3-1)!(5-1)!} = .00077.

Note that the probability of these data is very small. This is because there are many possible outcomes (namely 2^{10}) of tossing a thumbtack ten times. ■

Theorem 13.1 holds, even if a and b are not integers. We merely state the result here.

Theorem 13.2 Suppose we are about to repeatedly toss a thumbtack (or perform any repeatable experiment with two outcomes), we assume exchangeability, and we represent our prior belief concerning the probability of heads using a Dirichlet distribution with parameters a and b, where a and b are positive real numbers and m = a + b. Let D be data that consist of s heads and t tails in n trials. Then

P(D) = \frac{\Gamma(m)}{\Gamma(m+n)} \times \frac{\Gamma(a+s)\Gamma(b+t)}{\Gamma(a)\Gamma(b)}. (13.1)

Proof. The proof can be found in [Neapolitan, 2004]. ■

In the preceding theorem \(\Gamma\) denotes the gamma function. When \(n\) is an integer \(\ge 1\), we have that

\(\Gamma(n) = (n-1)!\).

So, the preceding theorem generalizes Theorem 13.1.

We developed the method for computing the probability of data for the case of binomial variables. It extends readily to multinomial variables. See [Neapolitan, 2004] for that extension.

## 13.2.1.2 Learning DAG Models Using the Bayesian Score

Next we show how we score a DAG model by computing the probability of the data given the model and how we use that score to learn a DAG model.

Suppose we have a Bayesian network for learning, as discussed in Section 12.2. For example, we might have the network in Figure 13.1 (a). Here we call such a network a DAG model. We can score a DAG model \(\mathbb{G}\) based on data D by determining how probable the data are given the DAG model. That is, we compute \(P(D|\mathbb{G})\). The formula for this probability is the same as that developed in Theorem 13.2, except there is a term of the form in Equality 13.1 for each probability in the network. So, the probability of data D given the DAG model \(\mathbb{G}_1\) in Figure 13.1 (a) is given by

\(\begin{aligned} P(D|\mathbb{G}_1) = \frac{\Gamma(m_{11})}{\Gamma(m_{11}+n_{11})} \times \frac{\Gamma(a_{11}+s_{11})\Gamma(b_{11}+t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \\ \frac{\Gamma(m_{21})}{\Gamma(m_{21}+n_{21})} \times \frac{\Gamma(a_{21}+s_{21})\Gamma(b_{21}+t_{21})}{\Gamma(a_{21})\Gamma(b_{21})} \times \\ \frac{\Gamma(m_{22})}{\Gamma(m_{22}+n_{22})} \times \frac{\Gamma(a_{22}+s_{22})\Gamma(b_{22}+t_{22})}{\Gamma(a_{22})\Gamma(b_{22})}. \end{aligned}\)

The data used in each term include only the data relevant to the conditional probability the term represents. This is exactly the same scheme that was used to learn parameters in Section 12.2. For example, the value of \(s_{21}\) is the number of cases that have \(J\) equal to \(j_2\) and \(F\) equal to \(f_1\).

Similarly, the probability of data D given the DAG model \(\mathbb{G}_2\) in Figure 13.1 (b) is given by

\(\begin{aligned} P(D|\mathbb{G}_2) = \frac{\Gamma(m_{11})}{\Gamma(m_{11}+n_{11})} \times \frac{\Gamma(a_{11}+s_{11})\Gamma(b_{11}+t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \\ \frac{\Gamma(m_{21})}{\Gamma(m_{21}+n_{21})} \times \frac{\Gamma(a_{21}+s_{21})\Gamma(b_{21}+t_{21})}{\Gamma(a_{21})\Gamma(b_{21})}. \end{aligned}\)

Note that the values of \(a_{11}, s_{11}\), and so on in Equality 13.3 are the ones relevant to \(\mathbb{G}_2\) and are not the same values as those in Equality 13.2. We have not explicitly shown their dependence on the DAG model, for the sake of notational simplicity.

Example 13.3 Suppose we want to determine whether job status (J) has a causal effect on whether someone defaults on a loan (F). Furthermore, we articulate just two values for each variable as follows:

![](img/67fa924962ee21b3590be9f3b10d9fe7_370_0.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_370_1.png)

Figure 13.1 The network in (a) models that J has a causal effect on F, whereas the network in (b) models that neither variable causes the other.

| Variable | Value | When the Variable Takes This Value |
|---|---|---|
| J | j1 | Individual is a white-collar worker |
| | j2 | Individual is a blue-collar worker |
| F | f1 | Individual has defaulted on a loan at least once |
| | f2 | Individual has never defaulted on a loan |

We represent the assumption that J has a causal effect on F with the DAG model G1 in Figure 13.1 (a) and the assumption that neither variable has a causal effect on the other with the DAG model G2 in Figure 13.1 (b). We assume that F does not have a causal effect on J, so we do not model this situation.

Suppose that next we obtain the data D in the following table:

| Case | J | F |
|---|---|---|
| 1 | j1 | f1 |
| 2 | j1 | f1 |
| 3 | j1 | f1 |
| 4 | j1 | f1 |
| 5 | j1 | f2 |
| 6 | j2 | f1 |
| 7 | j2 | f2 |
| 8 | j2 | f2 |

Then, owing to Equality 13.2,

P(D|G_1) = \frac{\Gamma(m_{11})}{\Gamma(m_{11} + n_{11})} \times \frac{\Gamma(a_{11} + s_{11})\Gamma(b_{11} + t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \frac{\Gamma(m_{21})}{\Gamma(m_{21} + n_{21})} \times \frac{\Gamma(a_{21} + s_{21})\Gamma(b_{21} + t_{21})}{\Gamma(a_{21})\Gamma(b_{21})} \times \frac{\Gamma(m_{22})}{\Gamma(m_{22} + n_{22})} \times \frac{\Gamma(a_{22} + s_{22})\Gamma(b_{22} + t_{22})}{\Gamma(a_{22})\Gamma(b_{22})} \\
= \frac{\Gamma(4)}{\Gamma(4 + 8)} \times \frac{\Gamma(2 + 5)\Gamma(2 + 3)}{\Gamma(2)\Gamma(2)} \times \frac{\Gamma(2)}{\Gamma(2 + 5)} \times \frac{\Gamma(1 + 4)\Gamma(1 + 1)}{\Gamma(1)\Gamma(1)} \times \frac{\Gamma(2)}{\Gamma(2 + 3)} \times \frac{\Gamma(1 + 1)\Gamma(1 + 2)}{\Gamma(1)\Gamma(1)} \\
= 7.2150 \times 10^{-6}.

Furthermore,

P(D|G_2) = \frac{\Gamma(m_{11})}{\Gamma(m_{11} + n_{11})} \times \frac{\Gamma(a_{11} + s_{11})\Gamma(b_{11} + t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \frac{\Gamma(m_{21})}{\Gamma(m_{21} + n_{21})} \times \frac{\Gamma(a_{21} + s_{21})\Gamma(b_{21} + t_{21})}{\Gamma(a_{21})\Gamma(b_{21})} \times \frac{\Gamma(m_{22})}{\Gamma(m_{22} + n_{22})} \times \frac{\Gamma(a_{22} + s_{22})\Gamma(b_{22} + t_{22})}{\Gamma(a_{22})\Gamma(b_{22})} \\
= \frac{\Gamma(4)}{\Gamma(4 + 8)} \times \frac{\Gamma(2 + 5)\Gamma(2 + 3)}{\Gamma(2)\Gamma(2)} \times \frac{\Gamma(4)}{\Gamma(4 + 8)} \times \frac{\Gamma(2 + 5)\Gamma(2 + 3)}{\Gamma(2)\Gamma(2)} \\
= 6.7465 \times 10^{-6}.

If our prior belief is that neither model is more probable than the other, we assign

P(G_1) = P(G_2) = .5.

Then, owing to Bayes' theorem,

P(G_1|D) = \frac{P(D|G_1)P(G_1)}{P(D|G_1)P(G_1) + P(D|G_2)P(G_2)} \\
= \frac{7.2150 \times 10^{-6} \times .5}{7.2150 \times 10^{-6} \times .5 + 6.7465 \times 10^{-6} \times .5} \\
= .517

and

$$P(\mathbb{G}_2|\mathbf{D}) = \frac{P(\mathbf{D}|\mathbb{G}_2)P(\mathbb{G}_2)}{P(\mathbf{D})}
= \frac{6.7465 \times 10^{-6}(.5)}{7.2150 \times 10^{-6} \times .5 + 6.7465 \times 10^{-6} \times .5}
= .483.$$

We select (learn) DAG $\mathbb{G}_1$ and conclude that it is more probable that job status does have a causal effect on whether someone defaults on a loan.

## 13.2.1.3 Learning DAG Patterns

The DAG $F \rightarrow J$ is Markov equivalent to the DAG in Figure 13.1 (a). Intuitively, we would expect it to have the same score. As long as we use a prior equivalent sample size (see Section 12.2.2), they will have the same score. This is discussed in [Neapolitan, 2004]. In general, we cannot distinguish Markov-equivalent DAGs based on data. So, we are actually learning Markov equivalence classes (DAG patterns) when we learn a DAG model from data.

## 13.2.1.4 Scoring Larger DAG Models

We illustrated Bayesian scoring using two variables. The general formula for the score when there are $n$ variables and the variables are binomial is as follows.

**Theorem 13.3** Suppose we have a DAG $\mathbb{G} = (\mathbf{V}, \mathbf{E})$ where $\mathbf{V}$ is a set of binomial random variables, we assume exchangeability, and we use a Dirichlet distribution to represent our prior belief for each conditional probability distribution of every variable in $\mathbf{V}$. Suppose further we have data $D$ consisting of a set of data items such that each data item is a vector of values of all the variables in $\mathbf{V}$. Then

$$P(\mathbf{D}|\mathbb{G}) = \prod_{i=1}^n \prod_{j=1}^{q_i} \frac{\Gamma(N_{ij})}{\Gamma(N_{ij} + M_{ij})} \frac{\Gamma(a_{ij} + s_{ij})\Gamma(b_{ij} + t_{ij})}{\Gamma(a_{ij})\Gamma(b_{ij})}$$ (13.4)

where

- 1. $n$ is the number of variables.
- 2. $q_i$ is the number of different instantiations of the parents of $X_i$.
- 3. $a_{ij}$ is our ascertained prior belief concerning the number of times $X_i$ took its first value when the parents of $X_i$ had their $j$th instantiation.
- 4. $b_{ij}$ is our ascertained value prior belief concerning the number of times $X_i$ took its second value when the parents of $X_i$ had their $j$th instantiation.
- 5. $s_{ij}$ is the number of times in the data that $X_i$ took its first value when the parents of $X_i$ had their $j$th instantiation.
