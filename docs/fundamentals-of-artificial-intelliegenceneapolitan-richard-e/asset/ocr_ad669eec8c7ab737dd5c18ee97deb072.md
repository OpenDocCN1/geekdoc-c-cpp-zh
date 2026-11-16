![](bbox=[0.22, 0.08, 0.82, 0.43])

Figure 12.4 Bayesian networks for parameter learning containing prior equivalent sample sizes.

Theorem 12.3 Suppose we specify a Bayesian network for parameter learning in the case of binomial variables and assign for all \(i\) and \(j\)

\(a_{ij} = b_{ij} = \frac{\alpha}{2q_i}\)

where \(N\) is a positive integer and \(q_i\) is the number of instantiations of the parents of the \(i\)th variable. Then the resultant Bayesian network has equivalent sample size \(\alpha\), and the joint probability distribution in the Bayesian network is uniform.

Figure 12.4 (a) shows a Bayesian network for parameter learning obtained using Theorem 12.3 with \(\alpha = 4\).

We developed the method for learning parameters in a Bayesian network in the case of binomial variables. It extends readily to multinomial variables. See [Neapolitan, 2004] for that extension.

# 12.3 Learning Parameters with Missing Data★

So far we have considered data sets in which every value of every variable is recorded in every case. Next, we consider the case where some data items might be omitted. How might they be omitted? A common way, and indeed a way that is relatively easy to handle, is that they are simply random omissions due to recording problems or some similar error. We present that case.