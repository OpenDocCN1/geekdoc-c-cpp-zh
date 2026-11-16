In the preceding theorem \(\Gamma\) denotes the gamma function. When \(n\) is an integer \(\ge 1\), we have that

\(\Gamma(n) = (n-1)!\).

So, the preceding theorem generalizes Theorem 13.1.

We developed the method for computing the probability of data for the case of binomial variables. It extends readily to multinomial variables. See [Neapolitan, 2004] for that extension.

# 13.2.1.2 Learning DAG Models Using the Bayesian Score

Next we show how we score a DAG model by computing the probability of the data given the model and how we use that score to learn a DAG model.

Suppose we have a Bayesian network for learning, as discussed in Section 12.2. For example, we might have the network in Figure 13.1 (a). Here we call such a network a DAG model. We can score a DAG model \(\mathbb{G}\) based on data D by determining how probable the data are given the DAG model. That is, we compute \(P(D|\mathbb{G})\). The formula for this probability is the same as that developed in Theorem 13.2, except there is a term of the form in Equality 13.1 for each probability in the network. So, the probability of data D given the DAG model \(\mathbb{G}_1\) in Figure 13.1 (a) is given by

\(\begin{aligned} P(D|\mathbb{G}_1) = \frac{\Gamma(m_{11})}{\Gamma(m_{11}+n_{11})} \times \frac{\Gamma(a_{11}+s_{11})\Gamma(b_{11}+t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \\ \frac{\Gamma(m_{21})}{\Gamma(m_{21}+n_{21})} \times \frac{\Gamma(a_{21}+s_{21})\Gamma(b_{21}+t_{21})}{\Gamma(a_{21})\Gamma(b_{21})} \times \\ \frac{\Gamma(m_{22})}{\Gamma(m_{22}+n_{22})} \times \frac{\Gamma(a_{22}+s_{22})\Gamma(b_{22}+t_{22})}{\Gamma(a_{22})\Gamma(b_{22})}. \end{aligned}\)

The data used in each term include only the data relevant to the conditional probability the term represents. This is exactly the same scheme that was used to learn parameters in Section 12.2. For example, the value of \(s_{21}\) is the number of cases that have \(J\) equal to \(j_2\) and \(F\) equal to \(f_1\).

Similarly, the probability of data D given the DAG model \(\mathbb{G}_2\) in Figure 13.1 (b) is given by

\(\begin{aligned} P(D|\mathbb{G}_2) = \frac{\Gamma(m_{11})}{\Gamma(m_{11}+n_{11})} \times \frac{\Gamma(a_{11}+s_{11})\Gamma(b_{11}+t_{11})}{\Gamma(a_{11})\Gamma(b_{11})} \times \\ \frac{\Gamma(m_{21})}{\Gamma(m_{21}+n_{21})} \times \frac{\Gamma(a_{21}+s_{21})\Gamma(b_{21}+t_{21})}{\Gamma(a_{21})\Gamma(b_{21})}. \end{aligned}\)

Note that the values of \(a_{11}, s_{11}\), and so on in Equality 13.3 are the ones relevant to \(\mathbb{G}_2\) and are not the same values as those in Equality 13.2. We have not explicitly shown their dependence on the DAG model, for the sake of notational simplicity.

Example 13.3 Suppose we want to determine whether job status (J) has a causal effect on whether someone defaults on a loan (F). Furthermore, we articulate just two values for each variable as follows: