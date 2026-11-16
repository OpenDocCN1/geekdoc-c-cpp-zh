where the superscript \( m \) on a parameter denotes the estimate of that parameter at the \( m^{th} \) iteration.

The denominator in the previous equation guarantees that \( \sum_{j=1}^K \gamma_{ij}^m = 1 \). With this constraint, we can be comfortable thinking of the \( \gamma \)’s as probabilities. In the following, we will usually drop the superscript \( m \), except on \( \gamma \), since all operations are performed identically at each iteration.

As in section 6.5.1, we usually deal with logarithms of probabilities rather than the probabilities themselves. This is because we almost always deal with random variables assumed to be independent. This independence means joint probabilities can be written as products, and their logarithms as sums. Operations that are easy on sums (e.g., differentiation) can be quite messy when attempted on products.

Denote by \( \theta \) the vector of parameters, including all the \( A \)’s, \( \mu \)’s, and all the \( \sigma \)’s. Initially, we simply choose some value for these variables, 1 and assume those values are correct. They are then updated as the algorithm runs.

Based on a single measurement, \( y_i \), we seek the expected value of \( \log p(y_i|\theta) \). Recall that the expected value of a random variable is a sum of the value of the random variable multiplied by its probability. Denote this value by \( Q_i(\theta|\theta^m) \), the expected value of the parameters, given the \( m^{th} \) estimate of those parameters, so that

```
\( Q(\theta|\theta^m) = \sum_{j=1}^K \gamma_{ij}^m \log A_j \Psi(y_i|\mu_j, \sigma_j) \)
\( = \sum_{j=1}^K \gamma_{ij}^m \left( \log A_j - \frac{1}{2} \log 2\pi - \log \sigma_j - \frac{(y_i - \mu_j)^2}{2\sigma_j^2} \right). \) (8.7)
```

It is not hard to show that if Eq. 8.7 holds for a single measurement, \( y_i \), then

```
\( Q(\theta|\theta^m) = \sum_{i=1}^n \sum_{j=1}^K \gamma_{ij}^m \left( \log A_j - \log \sigma_j - \frac{(y_i - \mu_j)^2}{2\sigma_j} \right) + C. \) (8.8)
```

where \( C \) is a constant that does not affect the maximization and hence can be dropped. To get the expectation into a more tractable form define

```
\( n_j^m = \sum_{i=1}^n \gamma_{ij}^m. \) (8.9)
```

Equation 8.9 allows us to separate the \( A \)’s from the \( \mu \)’s and the \( \sigma \)’s, writing

```
\( Q(\theta|\theta^m) = \sum_{j=1}^K n_j^m (\log A_j - \log \sigma_j) - \sum_{i=1}^n \sum_{j=1}^K \gamma_{ij}^m \frac{(y_i - \mu_j)^2}{2\sigma_j^2}. \) (8.10)
```

This equation concludes the E-step of the EM algorithm.

Now that we have \( Q(\theta|\theta^m) \) in a closed form, we find which values of the parameters maximize it. In this brief introduction, we illustrate the process by finding only the means, \( \mu_j \), leaving the estimation of the optimizing \( A \)’s and \( \sigma \)’s as exercises. First, we observe that