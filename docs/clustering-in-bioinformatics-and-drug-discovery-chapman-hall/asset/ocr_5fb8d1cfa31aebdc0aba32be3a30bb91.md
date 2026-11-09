but we speak of the expectation as an operator with specific properties, and rather than just a set of values from a sample, the expectation can operate on a function. Similarly the variance of the distribution is defined by

$$\operatorname{Var}[\mathbf{x}] = \mathbb{E}[(\mathbf{x}-\mu)^2], \tag{12.17}$$

and denoted as σ². The variance gives a measure of spread of the distribution. The standard deviation is simply the square root of the variance. With the standard deviation we can measure off the distribution in terms of distance from the mean, as so many standard deviations from the mean.

The concept of a random variable and probability can be generalized to the joint probability of two or more random variables. The covariance of two random variables expressed in vector form, x and y, gives the covariance matrix,

$$\Sigma = \mathbb{E}[(\mathbf{x}-\mu)(\mathbf{x}-\mu)^\mathsf{T}]. \tag{12.18}$$

This latter expression is exceptionally useful in a great many data applications.

# ### 12.3 Primer on Number Theory

Number theory was, until the mid-twentieth century, considered an area of pure mathematics unsullied by derivative applications. Today it is widely applied in areas of cryptography, computer science, and statistical modeling. It is remarkable how a mathematics that begins with the natural numbers and simple arithmetic proceeds to exceptionally sophisticated mathematics, bridging combinatorics, topology, and analysis among other mathematical fields; and it includes some of the most difficult and celebrated unsolved problems in mathematics today, such as the enormously deep Riemann's hypothesis, and the unbelievably simple to state Goldbach conjecture (the sum of any even positive integer greater than 3 is the sum of two prime numbers). This primer is mainly concerned with an introduction to elementary and analytical number theory sufficient to provide a grounding in its use within the confines of cluster analysis, which are few and rather specific. One such simple concept, that of the Farey sequence, is related to Riemann's hypothesis, independent of its application in cluster analysis. At the end of this section, this connection shown for the general bemusement of the reader.

The natural numbers and simple arithmetic have generally recognized facts: there are odd and even numbers, some are divisible, some are not, there are prime numbers, perfect numbers, square free numbers, twin primes (3 and 5, 5 and 7, 11 and 13, 17 and 19...), etc. Number theory begins with these simple facts and proceeds to theorems about these and related facts and assorted arithmetic axioms and extensions of the concepts of number and arithmetic. Simple questions arise (e.g., are there an infinite number of twin