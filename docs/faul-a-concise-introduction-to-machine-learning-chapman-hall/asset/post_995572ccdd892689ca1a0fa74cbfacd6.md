
be an envelope of $f$. The samples $\mathbf{x}_1, \dots, \mathbf{x}_n$ are drawn from the proposal distribution. Then

$$
\mathbb{E}_f[h] = \int h(\mathbf{x})f(\mathbf{x})d\mathbf{x} = \int h(\mathbf{x})\frac{f(\mathbf{x})}{g(\mathbf{x})}g(\mathbf{x})d\mathbf{x} = \mathbb{E}_g[hf/g] \approx \frac{1}{N}\sum_{n=1}^N \frac{f(\mathbf{x}_n)}{g(\mathbf{x}_n)}h(\mathbf{x}_n),
$$

where we used subscripts to indicate with respect to which probability density function the expectation is taken. All generated samples, unlike rejection sampling, are used. The factors $f(\mathbf{x}_n)/g(\mathbf{x}_n)$ are known as *importance weights*. They are a correction to sampling from the wrong distribution. For example, if $g$ follows $f$ in a region, this factor is one and no correction is necessary. If, however, $g$ is large in a region where $f$ is small, the contribution of evaluating $h$ there needs to be reduced. On the other hand, if $g$ is small in a region where $f$ is large and we happen to sample there, the value of $h$ there needs to be magnified.

In the case when

$$
f(\mathbf{x}) = \frac{1}{c_f}\hat{f}(\mathbf{x}) \text{ and } g(\mathbf{x}) = \frac{1}{c_g}\hat{g}(\mathbf{x})
$$

and the normalizing constants

$$
c_f = \int \hat{f}(\mathbf{x})d\mathbf{x} \text{ and } c_g = \int \hat{g}(\mathbf{x})d\mathbf{x}
$$

are unknown, the calculation becomes

$$
\mathbb{E}_f[h] = \int h(\mathbf{x})f(\mathbf{x})d\mathbf{x} = \frac{c_g}{c_f} \int h(\mathbf{x})\frac{\hat{f}(\mathbf{x})}{\hat{g}(\mathbf{x})}g(\mathbf{x})d\mathbf{x} = \frac{c_g}{c_f}\mathbb{E}_g[h\hat{f}/\hat{g}] \approx \frac{c_g}{c_f}\frac{1}{N}\sum_{n=1}^N \frac{\hat{f}(\mathbf{x}_n)}{\hat{g}(\mathbf{x}_n)}h(\mathbf{x}_n).
$$

Even though the normalizing constants are unknown, we can estimate their ratio. Using $c_g = \hat{g}(\mathbf{x})/g(\mathbf{x})$ wherever $g(\mathbf{x})$ is nonzero, we have

$$
\frac{c_f}{c_g} = \frac{1}{c_g} \int \hat{f}(\mathbf{x})d\mathbf{x} = \int \frac{\hat{f}(\mathbf{x})}{\hat{g}(\mathbf{x})}g(\mathbf{x})d\mathbf{x} = \mathbb{E}_g[\hat{f}/\hat{g}] \approx \frac{1}{N}\sum_{n=1}^N \frac{\hat{f}(\mathbf{x}_n)}{\hat{g}(\mathbf{x}_n)}.
$$

With this result, the expectation is estimated as

$$
\mathbb{E}_f[h] \approx \frac{1}{\sum_{k=1}^N \hat{f}(\mathbf{x}_k)/\hat{g}(\mathbf{x}_k)} \sum_{n=1}^N \frac{\hat{f}(\mathbf{x}_n)}{\hat{g}(\mathbf{x}_n)}h(\mathbf{x}_n).
$$

The importance weights are

$$
w_n = \frac{\hat{f}(\mathbf{x}_n)/g(\mathbf{x}_n)}{\sum_{k=1}^N \hat{f}(\mathbf{x}_k)/g(\mathbf{x}_k)} = \frac{\hat{f}(\mathbf{x}_n)/g(\mathbf{x}_n)}{\sum_{k=1}^N \hat{f}(\mathbf{x}_k)/g(\mathbf{x}_k)}, \quad (3.4)
$$

since \( g \) and \( \tilde{g} \) only differ by a multiplicative constant. Note that if the proposal distribution coincides with \( f \), then we have \( w_n = 1/N \).

As with rejection sampling, the choice of the proposal distribution is crucial. Most importantly, it should not be small in regions where \( f \) is large. The weighting can only make a correction if an actual sample is drawn from this region.

Sampling-importance-resampling (SIR) combines ideas from rejection sampling and importance sampling. First, \( N \) samples \( \mathbf{x}_1, \dots, \mathbf{x}_N \) are drawn from the proposal distribution \( g \). Instead of rejecting some of them, weights are calculated according to (3.4). Then \( N \) samples are drawn from the discrete sample \( \{\mathbf{x}_1, \dots, \mathbf{x}_N\} \) according to the probabilities given by \( w_1, \dots, w_N \). Thus a sample can feature several times in the final set, if its weight is larger than the weights of the other samples. If \( g = f \), then all weights will equal \( 1/N \) and all samples are equally likely to be drawn.

## 3.4 Markov Chains

Markov chains are an important building block for a class of sampling algorithms which can be applied to many different distributions and also scale well with dimensionality.

A Markov chain is a series of random variables \( \mathbf{x}_1, \dots, \mathbf{x}_N \). The indices are associated with a sequence in time. A Markov chain of order \( m \) satisfies the following property

\( p(\mathbf{x}_n|\mathbf{x}_{n-1}, \mathbf{x}_{n-2}, \dots, \mathbf{x}_1) = p(\mathbf{x}_n|\mathbf{x}_{n-1}, \mathbf{x}_{n-2}, \dots, \mathbf{x}_{n-m}) \)

for \( n = m + 1, \dots, M \). This means the \( n^{th} \) random variable only depends on the \( m \) previous variables. In particular, a first-order Markov chain satisfies

\( p(\mathbf{x}_n|\mathbf{x}_{n-1}, \mathbf{x}_{n-2}, \dots, \mathbf{x}_1) = p(\mathbf{x}_n|\mathbf{x}_{n-1}) \)

Each random variable only depends on its predecessor. We will only consider first-order Markov chains, since any Markov chain of order \( m \) can be transcribed into a first-order Markov chain by letting \( \mathbf{y}_{n-m+1} \) be the tuple \( (\mathbf{x}_n, \dots, \mathbf{x}_{n-m+1}) \), then since \( p(\mathbf{y}_k|\mathbf{y}_{k-1}, \dots, \mathbf{y}_1) = p(\mathbf{y}_k|\mathbf{y}_{k-1}) \).

The probabilities \( T_n(\mathbf{x}_{n-1}, \mathbf{x}_n) = p(\mathbf{x}_n|\mathbf{x}_{n-1}) \) are called transition probabilities. If they are the same for all \( n \), i.e. \( T_n(\mathbf{x}_{n-1}, \mathbf{x}_n) = T(\mathbf{x}_{n-1}, \mathbf{x}_n) \) for all \( n \), then the Markov chain is called homogeneous.

Graphically, a first-order Markov chain can be represented as

![](img/d3c00252180686426c9e63ab889b535b_95_0.png)

The possible values of \( \mathbf{x}_n \) form a state space. We distinguish between a discrete and countable, possibly finite state space, and a continuous state space, which is sometimes called general state space. Summing or integrating over all possible states \(\mathbf{x}_{n-1}\) gives the marginal probability of \(\mathbf{x}_n\),

\(p(\mathbf{x}_n) = \sum_{\mathbf{x}_{n-1}} p(\mathbf{x}_n | \mathbf{x}_{n-1}) p(\mathbf{x}_{n-1})\) or \(p(\mathbf{x}_n) = \int p(\mathbf{x}_n | \mathbf{x}_{n-1}) p(\mathbf{x}_{n-1}) d\mathbf{x}_{n-1}\).

To do so the marginal probability of \(\mathbf{x}_{n-1}\) needs to be known. Starting from the initial distribution \(p(\mathbf{x}_1)\), all marginal distributions can be calculated.

For a homogeneous Markov chain, the transition probabilities can be completely described by noting how T acts on different elements of the state space, \(T(\mathbf{x}, \hat{\mathbf{x}})\) for all states \(\mathbf{x}\) and \(\hat{\mathbf{x}}\).

A Markov chain is called *irreducible*, if the probability of reaching state \(\mathbf{x}\) from state \(\hat{\mathbf{x}}\) in a finite number of steps is non-zero for all states \(\mathbf{x}\) and \(\hat{\mathbf{x}}\). In other words, any state can be reached from any other state in a finite number of steps.

A distribution specified by the probability mass function or probability density function \(f\) is called *invariant* or *stationary* with respect to the Markov chain; if \(\mathbf{x}_{n-1}\) follows the distribution, then so does \(\mathbf{x}_n\) for all \(n\). In other words, if \(\mathbf{x}_0\) follows the distribution, then so does the complete chain. The distribution remains the same after each step. Note that several distributions can be invariant with respect to a given Markov chain. For example, in the degenerate case where

\(T(\mathbf{x}, \hat{\mathbf{x}}) = \begin{cases} 1 & \text{if } \hat{\mathbf{x}} = \mathbf{x}, \\ 0 & \text{otherwise,} \end{cases}\)

we have \(\mathbf{x}_1 = \mathbf{x}_2 = \cdots = \mathbf{x}_N\). The transition in each step is the identity. In this case, any distribution is invariant.

For a homogeneous Markov chain, a distribution specified by \(f\) is invariant, if

\(f(\hat{\mathbf{x}}) = \sum_{\mathbf{x}} T(\mathbf{x}, \hat{\mathbf{x}}) f(\mathbf{x})\) or \(f(\hat{\mathbf{x}}) = \int T(\mathbf{x}, \hat{\mathbf{x}}) f(\mathbf{x}) d\mathbf{x}\),

where the sum or integral is over the state space.

It is possible to construct a Markov chain with transition probabilities such that a given \(f\) is invariant. To achieve this, the transition probabilities need to satisfy the property of *detailed balance*, for all pairs of states \(\mathbf{x}\) and \(\hat{\mathbf{x}}\):

\(T(\mathbf{x}, \hat{\mathbf{x}}) f(\mathbf{x}) = T(\hat{\mathbf{x}}, \mathbf{x}) f(\hat{\mathbf{x}})\).

Note that for \(\mathbf{x} = \hat{\mathbf{x}}\), the above equation is naturally true. If detailed balance is satisfied, the Markov chain is called *reversible*. Invariance is shown by

\(\sum_{\mathbf{x}} T(\mathbf{x}, \hat{\mathbf{x}}) f(\mathbf{x}) = \sum_{\hat{\mathbf{x}}} T(\hat{\mathbf{x}}, \mathbf{x}) f(\hat{\mathbf{x}}) = f(\hat{\mathbf{x}}) \sum_{\mathbf{x}} p(\mathbf{x} | \hat{\mathbf{x}}) = f(\hat{\mathbf{x}})\),

since the sum over the state space of the conditional probabilities is one. The calculation for a continuous probability density function \(f\) uses integrals and is analogous.

The transition probabilities can be constructed as linear combinations of base transition probabilities \(B_1, \dots, B_M\),
