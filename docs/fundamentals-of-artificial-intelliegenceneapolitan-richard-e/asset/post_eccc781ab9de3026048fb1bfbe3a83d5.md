
Table 14.1 Comparisons of Performance of Several Bandit Strategies

| Strategy | R-100 | R-1000 | R-10,000 | N-130 | BN-1300 |
|---|---|---|---|---|---|
| POKER | .787 | .885 | .942 | 203 | 132 |
| | | | | | |
| ε-Greedy, .05 | .712 | .855 | .936 | 733 | 431 |
| ε-Greedy, .10 | .740 | .858 | .916 | 731 | 453 |
| ε-Greedy, .15 | .746 | .842 | .891 | 715 | 474 |
| | | | | | |
| ε-First, .05 | .732 | .906 | .951 | 735 | 414 |
| ε-First, .10 | .802 | .893 | .926 | 733 | 421 |
| ε-First, .15 | .809 | .869 | .901 | 725 | 411 |
| | | | | | |
| ε-Decreasing, 1 | .755 | .805 | .851 | 738 | 411 |
| ε-Decreasing, 5 | .785 | .895 | .934 | 715 | 413 |
| ε-Decreasing, 10 | .736 | .901 | .949 | 733 | 417 |
| | | | | | |
| ε-LeastTaken, .05 | .750 | .782 | .932 | 747 | 420 |
| ε-LeastTaken, .10 | .750 | .791 | .912 | 738 | 432 |
| ε-LeastTaken, .15 | .757 | .784 | .892 | 734 | 441 |

For the R-experiment, bigger numbers are better (rewards), and for the N-experiments, smaller numbers are better (punishments).

In the first experiment, they simulated 1000 levers, where the reward associated with each lever was normally distributed. The means and standard deviations were drawn uniformly from the interval (0,1). They then generated a data set containing 10,000 rounds, and they evaluated the strategies using 100 rounds, 1000 rounds, and all 10,000 of the rounds. They computed the average reward per round for each strategy. This process was repeated 10,000 times and the averages over all 10,000 trials was computed.

The second experiment concerns the real-world problem known as the Content Distribution Network Problem (CDN) [Krishnamurthy et al., 2001]. The problem is to retrieve data through a network with several redundant sources available. For each retrieval, one source is selected, and the algorithm then waits until the data are retrieved. The objective is to minimize the sum of the delays over all retrievals. To simulate this problem, they used the home pages of over 700 universities as sources. The universities represent the levers. The home page for each university was retrieved every 10 minutes for 10 days, resulting in 1300 rounds. For each retrieval, the retrieval latency in milliseconds was recorded. This latency was the punishment. The strategies were evaluated using 130 rounds and all 1300 rounds. They computed the average latency (punishment) per round for each strategy.

For both experiments, the process was repeated 10,000 times and the averages over all 10,000 trials was computed. Table 14.1 shows the results for POKER and the four strategies presented here. For the R-experiments, bigger numbers are better because they represent rewards, whereas for the N-experiments smaller numbers are better because they represent punishments. Vermorel and Mohri [2005] include results for some other strategies. Interesting is that all the strategies perform similarly for the R-experiments, but POKER does much better for the N-experiments (which are real-world). This result remains true when we include the additional results in [Vermorel and Mohri, 2005].

## 14.2.2 Dynamic Networks★

Dynamic Bayesian networks model relationships among random variables that change over time. Dynamic Influence diagrams model sequential decision making based on observing variables over time. So the latter can be used for reinforcement learning. Before discussing dynamic influence diagrams and their application to reinforcement learning, we present Dynamic Bayesian networks.

### 14.2.2.1 Dynamic Bayesian Networks

After developing the theory, we present an example.

**Formulation of the Theory** Bayesian networks do not model temporal relationships among variables. That is, a Bayesian network only represents the probabilistic relationships among a set of variables at some point in time. It does not represent how the value of some variable may be related to its value and the values of other variables at previous points in time. In many problems, however, the ability to model temporal relationships is very important. For example, in medicine it is often important to represent and reason about time in tasks such as diagnosis, prognosis, and treatment options. Capturing the dynamic (temporal) aspects of the problem is also important in artificial intelligence, economics, and biology. Next, we introduce dynamic Bayesian networks, which do model the temporal aspects of a problem.

```
$$\mathbf{X} = \begin{pmatrix} X_1 \\ \vdots \\ X_n \end{pmatrix}$$
```

is called a **random vector**. A **random matrix** is defined in the same manner. We use **X** to denote both a random vector and the set of random variables that comprises **X**. Similarly, we use **x** to denote both a vector value of **X** and the set of values that comprises **x**. The meaning is clear from the context. Given this convention and a random vector **X** with dimension \(n\), \(P(\mathbf{x})\) denotes the joint probability distribution \(P(x_1, ..., x_n)\). Random vectors are called **independent** if the sets of variables that comprise them are independent. A similar definition holds for conditional independence.

Now we can discuss dynamic Bayesian networks. We assume that changes occur between discrete time points, which are indexed by the non-negative integers, and we have some finite number \( T \) of points in time. Let \(\{X_1, \dots, X_n\}\) be the set of features whose values change over time, let \(X_i[t]\) be a random variable representing the value of \(X_i\) at time \(t\) for \(0 \le t \le T\), and let the random vector \(\mathbf{X}[t]\) be given by

```
\(\mathbf{X}[t] = \begin{pmatrix} X_1[t] \\ \vdots \\ X_n[t] \end{pmatrix}.\)
```

For all \(t\), each \(X_i[t]\) has the same space that depends on \(i\), and we call it the space of \(X_i\). A **dynamic Bayesian network** is a Bayesian network containing the variables that comprise the \(T\) random vectors \(\mathbf{X}[t]\) and is determined by the following specifications:

- 1. An initial Bayesian network consisting of (a) an initial DAG \(\mathbb{G}_0\) containing the variables in \(\mathbf{X}[0]\) and (b) an initial probability distribution \(P_0\) of these variables.

- 2. A transition Bayesian network, which is a template consisting of (a) a transition DAG \(\mathbb{G}_-\) containing the variables in \(\mathbf{X}[t] \cup \mathbf{X}[t+1]\) and (b) a transition probability distribution \(P_-\), that assigns a conditional probability to every value of \(\mathbf{X}[t+1]\) given every value \(\mathbf{X}[t]\). That is, for every value \(\mathbf{x}[t+1]\) of \(\mathbf{X}[t+1]\) and value \(\mathbf{x}[t]\) of \(\mathbf{X}[t]\), we specify

```
\(P_-(\mathbf{X}[t+1] = \mathbf{x}[t+1] | \mathbf{X}[t] = \mathbf{x}[t]).\)
```

Because for all \(t\) each \(X_i\) has the same space, the vectors \(\mathbf{x}[t+1]\) and \(\mathbf{x}[t]\) each represent values from the same set of spaces. The index in each indicates the random variable that has the value. We showed the random variables above; henceforth we do not show them.

- 3. The dynamic Bayesian network consisting of (a) the DAG composed of the DAG \(\mathbb{G}_0\) and for \(0 \le t \le T-1\) the DAG \(\mathbb{G}_-\) evaluated at \(t\) and (b) the following joint probability distribution:

```
\(P(\mathbf{x}[0], \dots \mathbf{x}[T]) = P_0(\mathbf{x}[0]) \prod_{t=0}^{T-1} P_-(\mathbf{x}[t+1]|\mathbf{x}[t]).\) (14.1)
```

Figure 14.2 shows an example. The transition probability distribution entailed by the network in Figure 14.2 is

```
\(P_-(\mathbf{x}[t+1]|\mathbf{x}[t]) = \prod_{i=0}^n P_-(x_i[t+1]|\mathbf{pa}_i[t+1]),\)
```

where \(\mathbf{pa}_i[t+1]\) denotes the values of the parents of \(X_i[t+1]\). Note that there are parents in both \(\mathbf{X}[t]\) and \(\mathbf{X}[t+1]\).

Owing to Equality 14.1, for all \(t\) and all \(\mathbf{x}\),

```
\(P(\mathbf{x}[t+1]|\mathbf{x}[0], \dots \mathbf{x}[t]) = P(\mathbf{x}[t+1]|\mathbf{x}[t]).\)
```

![](img/67fa924962ee21b3590be9f3b10d9fe7_438_0.png)

**Figure 14.2** Prior and transition Bayesian networks are in (a). The resultant dynamic Bayesian network for $T=2$ is in (b). Note that the probability distributions are not shown.

That is, all the information needed to predict a world state at time $t$ is contained in the description of the world at time $t-1$. No information about earlier times is needed. Owing to this feature, we say the process has the **Markov** property. Furthermore, the process is **stationary**. That is, $P(\mathbf{x}[t+1]|\mathbf{x}[t])$ is the same for all \(t\). In general, it is not necessary for a dynamic Bayesian network to have either of these properties. However, they reduce the complexity of representing and evaluating the networks, and they are reasonable assumptions in many applications. The process need not stop at a particular time \(T\). However, in practice, we reason only about some finite amount of time. Furthermore, we need a terminal time value to properly specify a Bayesian network.

Probabilistic inference in a dynamic Bayesian network can be done using the standard algorithms discussed in Chapter 3. However, because the size of a dynamic Bayesian network can become enormous when the process continues for a long time, the algorithms can be quite inefficient. There is a special subclass of dynamic Bayesian networks in which this computation can be done more efficiently. This subclass includes dynamic Bayesian networks in which the networks in different time steps are connected only through non-evidence variables. An example of such a network is shown in Figure 14.3. The variables labeled with an \(E\) are the evidence variables and are instantiated in each time step. We lightly shade nodes representing them.

An application that uses a dynamic Bayesian network like the one in Figure 14.3. is shown in the next subsection. Presently, we illustrate how updating can be done effectively in such networks.
