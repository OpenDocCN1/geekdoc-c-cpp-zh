
then the resultant P satisfies Equality 13.12. Toward determining such values, let Q be the transition matrix of an arbitrary Markov chain whose states are the members of our given finite set of states \(\{e_1, e_2, \dots e_s\}\), and let

\[
\alpha_{ij} = \left\{ \begin{array}{ll} \frac{s_{ij}}{1 + \frac{r_i q_{ij}}{r_j q_{ji}}} & q_{ij} \neq 0, q_{ji} \neq 0 \\ 0 & q_{ij} = 0 \text{ or } q_{ji} = 0 \end{array} \right. \tag{13.14}
\]

where \(s_{ij}\) is a symmetric function of \(i\) and \(j\) chosen so that \(0 \le \alpha_{ij} \le 1\) for all \(i\) and \(j\). We then take

\[
p_{ij} = \alpha_{ij} q_{ij} \quad i \neq j \tag{13.15}
\]
\[
p_{ii} = 1 - \sum_{j \neq i} p_{ij}.
\]

It is straightforward to show that the resultant values of \(p_{ij}\) satisfy Equality 13.13. The irreducibility of P must be checked in each application.

Hastings [1970] suggests the following way of choosing s: If \(q_{ij}\) and \(q_{ji}\) are both nonzero, set

\[
s_{ij} = \left\{ \begin{array}{ll} 1 + \frac{r_i q_{ij}}{r_j q_{ji}} & \frac{r_j q_{ji}}{r_i q_{ij}} \ge 1 \\ 1 + \frac{r_j q_{ji}}{r_i q_{ij}} & \frac{r_j q_{ji}}{r_i q_{ij}} \le 1 \end{array} \right. \tag{13.16}
\]

Given this choice, we have

\[
\alpha_{ij} = \left\{ \begin{array}{ll} 1 & q_{ij} \neq 0, q_{ji} \neq 0, \frac{r_j q_{ji}}{r_i q_{ij}} \ge 1 \\ \frac{r_j q_{ji}}{r_i q_{ij}} & q_{ij} \neq 0, q_{ji} \neq 0, \frac{r_j q_{ji}}{r_i q_{ij}} \le 1 \\ 0 & q_{ij} = 0 \text{ or } q_{ji} = 0 \end{array} \right. \tag{13.17}
\]

If we make Q symmetric (that is, \(q_{ij} = q_{ji}\) for all \(i\) and \(j\)), we have the method devised by Metropolis et al. (1953). In this case

\[
\alpha_{ij} = \left\{ \begin{array}{ll} 1 & q_{ij} \neq 0, r_j \ge r_i \\ r_j / r_i & q_{ij} \neq 0, r_j \le r_i \\ 0 & q_{ij} = 0 \end{array} \right. \tag{13.18}
\]

Note that with this choice if Q is irreducible, so is P.

**Example 13.13** Suppose \(r^T = (1/8\ 3/8\ 1/2)\). Choose Q symmetric as follows:

Q =

| 1/3 | 1/3 | 1/3 |
| --- | --- | --- |
| 1/3 | 1/3 | 1/3 |
| 1/3 | 1/3 | 1/3 |

Choose s according to Equality 13.16 so that \(\alpha\) has the values in Equality 13.18. We then have

\(\alpha =\)

| 1 | 1 | 1 |
| --- | --- | --- |
| 1/3 | 1 | 1 |
| 1/4 | 3/4 | 1 |

Using Equality 13.15 we have

P =

| 1/3 | 1/3 | 1/3 |
| --- | --- | --- |
| 1/9 | 5/9 | 1/3 |
| 1/12 | 1/4 | 2/3 |

Notice that

\(r^T P = (1/8\ 3/8\ 1/2) \begin{pmatrix} 1/3 & 1/3 & 1/3 \\ 1/9 & 5/9 & 1/3 \\ 1/12 & 1/4 & 2/3 \end{pmatrix} = (1/8\ 3/8\ 1/2) = r^T\),

as it should.

Once we have constructed matrices Q and \(\alpha\) as discussed above, we can conduct the simulation as follows:

- 1. Given the state occupied at the kth trial is e_i, choose a state using the probability distribution given by the ith row of Q. Suppose that state is e_j.
- 2. Choose the state occupied at the (k + 1)st trial to be e_j with probability \(\alpha_{ij}\) and to be e_i with probability \(1 - \alpha_{ij}\).

In this way, when state e_i is the current state, e_j will be chosen q_{ij} fraction of the time in Step (1), and of those times e_j will be chosen \(\alpha_{ij}\) fraction of the time in Step (2). So overall, e_j will be chosen \(\alpha_{ij} q_{ij} = p_{ij}\) fraction of the time (see Equality 13.15), which is what we want.

## Gibbs Sampling Method

Next we show another method for creating a Markov chain whose stationary distribution is a particular joint probability distribution. The method is called Gibbs sampling, and it concerns the case where we have n random variables X_1, X_2, ... X_n and a joint probability distribution P of the variables (as in a Bayesian network). If we let X = {X_1, X_2, ... X_n}, we want to approximate

\(\sum_x f(x)P(x)\).

To approximate this sum using MCMC, we need to create a Markov chain whose set of states is all possible values of X, and whose stationary distribution is P(x). We do this by choosing the value of X in the hth trial as follows:

- Pick \(x_1^{(h)}\) using the distribution \(P(x_1|x_2^{(h-1)}, x_3^{(h-1)}, \dots, x_n^{(h-1)})\).
- Pick \(x_2^{(h)}\) using the distribution \(P(x_2|x_1^{(h)}, x_3^{(h-1)}, \dots, x_n^{(h-1)})\).
- \(\vdots\)
- Pick \(x_k^{(h)}\) using the distribution \(P(x_k|x_1^{(h)}, \dots, x_{k-1}^{(h)}, x_{k+1}^{(h-1)} \dots, x_n^{(h-1)})\).
- \(\vdots\)
- Pick \(x_n^{(h)}\) using the distribution \(P(x_n|x_1^{(h)}, \dots, x_{n-1}^{(h)})\).

Notice that in the kth step, all variables except \(x_k^{(h)}\) are unchanged, and the new value of \(x_k^{(h)}\) is drawn from its distribution conditional on the current values of all the other variables.

As long as all conditional probabilities are nonzero, the chain is irreducible. Next we verify that P(x) is the stationary distribution for the chain. If we let \(p(x;\hat{x})\) denote the transition probability from x to \(\hat{x}\) in each trial, we need to show that

\(P(\hat{x}) = \sum_x P(x)p(x;\hat{x})\). (13.19)

It is not hard to see that it suffices to show that Equality 13.19 holds for each step of each trial. To that end, for the kth step we have

\(\sum_x P(x)p_k(x;\hat{x})\)
\(= \sum_{x_1, \dots, x_n} P(x_1, \dots, x_n)p_k(x_1, \dots, x_n; \hat{x}_1, \dots, \hat{x}_n)\)
\(= \sum_{x_k} P(\hat{x}_1, \dots, \hat{x}_{k-1}, x_k, \hat{x}_{k+1}, \dots, \hat{x}_n)P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n) \sum_{x_k} P(\hat{x}_1, \dots, \hat{x}_{k-1}, x_k, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n)P(\hat{x}_1, \dots \hat{x}_{k-1}, \hat{x}_{k+1}, \dots \hat{x}_n)\)
\(= P(\hat{x}_1, \dots \hat{x}_{k-1}, \hat{x}_k, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x})\).

The second step follows because \(p_k(x;\hat{x}) = 0\) unless \(\hat{x}_j = x_j\) for all \(j \neq k\).

See [Geman and Geman, 1984] for more on Gibbs sampling.

### 13.2.6.3 Learning with Missing Data Using Gibbs Sampling

The Gibbs sampling approach we use is called the Candidate method (See [Chib, 1995]). The approach proceeds as follows: Let D be the set of values of the variables for which we have values. By Bayes' theorem we have

\[
P(\mathbf{D}|\mathbb{G}) = \frac{P(\mathbf{D}|\breve{\mathbf{f}}^{(\mathbb{G})}, \mathbb{G})\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbb{G})}{\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G})}, \tag{13.20}
\]

where \(\breve{\mathbf{f}}^{(\mathbb{G})}\) is an arbitrary assignment of values to the parameters in \(\mathbb{G}\). To approximate \(P(\mathbf{D}|\mathbb{G})\), we choose some value of \(\breve{\mathbf{f}}^{(\mathbb{G})}\), evaluate the numerator in Equality 13.20 exactly, and approximate the denominator using Gibbs sampling. For the denominator, we have

\[
\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G}) = \sum_{\mathbf{m}} \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbf{m}, \mathbb{G})P(\mathbf{m}|\mathbf{D}, \mathbb{G})
\]

where M is the set of variables that has missing values.

To approximate this sum using Gibbs sampling, we do the following:

- 1. Initialize the state of the unobserved variables to arbitrary values yielding a complete data set D1.
- 2. Choose some unobserved variable \(X_i^{(h)}\) arbitrarily and obtain a value of \(X_i^{(h)}\) using
  
  \[
  P(x'_i^{(h)}|\mathbf{D}_1 - \{\breve{x}_i^{(h)}\}, \mathbb{G}) = \frac{P(x'_i^{(h)}, \mathbf{D}_1 - \{\breve{x}_i^{(h)}\}|\mathbb{G})}{\sum_{x_i^{(h)}} P(x_i^{(h)}, \mathbf{D}_1 - \{\breve{x}_i^{(h)}\}|\mathbb{G})}
  \]
  
  where \(\breve{x}_i^{(h)}\) is the value of \(X_i^{(h)}\) in D1, and the sum is over all values in the space of \(X_i^{(h)}\). The terms in the numerator and denominator can be computed using Equality 13.4.
- 3. Repeat Step (2) for all the other unobserved variables, where the complete data set used in the (k+1)st iteration contains the values obtained in the previous k iterations.

This will yield a new complete data set D2.

- 4. Iterate the previous two steps some number R times where the complete data set from the jth iteration is used in the (j+1)st iteration. In this manner R complete data sets will be generated. For each complete data set \(\mathbf{D}_j\), compute
  
  \[
  \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}_j, \mathbb{G})
  \]
  
  using Equality 12.3.
- 5. Approximate
  
  \[
  \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G}) \approx \frac{\sum_{j=1}^R \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}_j, \mathbb{G})}{R}.
  \]

Although the Candidate method can be applied with any value of \(\breve{\mathbf{f}}^{(\mathbb{G})}\) of the parameters, some assignments lead to faster convergence. Chickering and Heckerman [1997] discuss methods for choosing the value.
