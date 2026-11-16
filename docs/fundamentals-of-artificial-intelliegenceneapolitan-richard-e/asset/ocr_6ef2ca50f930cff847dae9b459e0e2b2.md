ger numbers are better because they represent rewards, whereas for the N-experiments smaller numbers are better because they represent punishments. Vermorel and Mohri [2005] include results for some other strategies. Interesting is that all the strategies perform similarly for the R-experiments, but POKER does much better for the N-experiments (which are real-world). This result remains true when we include the additional results in [Vermorel and Mohri, 2005].

# 14.2.2 Dynamic Networks★

Dynamic Bayesian networks model relationships among random variables that change over time. Dynamic Influence diagrams model sequential decision making based on observing variables over time. So the latter can be used for reinforcement learning. Before discussing dynamic influence diagrams and their application to reinforcement learning, we present Dynamic Bayesian networks.

# 14.2.2.1 Dynamic Bayesian Networks

After developing the theory, we present an example.

**Formulation of the Theory** Bayesian networks do not model temporal relationships among variables. That is, a Bayesian network only represents the probabilistic relationships among a set of variables at some point in time. It does not represent how the value of some variable may be related to its value and the values of other variables at previous points in time. In many problems, however, the ability to model temporal relationships is very important. For example, in medicine it is often important to represent and reason about time in tasks such as diagnosis, prognosis, and treatment options. Capturing the dynamic (temporal) aspects of the problem is also important in artificial intelligence, economics, and biology. Next, we introduce dynamic Bayesian networks, which do model the temporal aspects of a problem.

```
$$\mathbf{X} = \begin{pmatrix} X_1 \\ \vdots \\ X_n \end{pmatrix}$$
```

is called a **random vector**. A **random matrix** is defined in the same manner. We use **X** to denote both a random vector and the set of random variables that comprises **X**. Similarly, we use **x** to denote both a vector value of **X** and the set of values that comprises **x**. The meaning is clear from the context. Given this convention and a random vector **X** with dimension \(n\), \(P(\mathbf{x})\) denotes the joint probability distribution \(P(x_1, ..., x_n)\). Random vectors are called **independent** if the sets of variables that comprise them are independent. A similar definition holds for conditional independence.

Now we can discuss dynamic Bayesian networks. We assume that changes occur between discrete time points, which are indexed by the non-negative