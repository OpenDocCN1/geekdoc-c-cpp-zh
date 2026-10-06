An emphasis on the academic community is truly model-free RL, and most of the theory builds on the optimal concepts reviewed in the next chapter. Some of the main ideas can be exposed here right.

What follows is background on how RL algorithms are currently formulated. Think hard about alternatives - remember, the field remains young!

# 2.5.1 Actors and Critics

The actor-critic algorithm of reinforcement learning is specifically designed within the context of stochastic control, so this is a topic for Part II. The origins of the terms are worth explaining here. We are given a parameterized family of functions $\{\phi^	heta : \theta \in \mathbb{R}^d\}$, which play the role of actors. For each $	heta$, we (or our "software agents") can observe features of the state process $x$ under chosen policy. The ideal critic computes the associated value function $J_	heta$, but in realistic situations we have only an estimate.

Since in this book we are minimizing cost rather than maximizing reward, the output of an actor-critic algorithm is

```
$$\theta^* = \arg_{\theta}(v, J_	heta),$
```

where $v \geq 0$ serves as a state weighting. This will be defined as a sum

```
$$\langle v, J_	heta\rangle = \sum_i J_	heta(x^i)v(x^i),$
```

where $v(x^i)$ is relatively large for "important states."
Methods to solve the optimization problem (2.51) are explored in Section 4.6, using an approach known as *gradient free optimization*. These algorithms are intended to approximate the true gradient descent algorithms of optimization surveyed in Section 4.4, and are often called "actor-only methods.\ The meaning of actor-critic methods is explained in Chapter 10.
This is an example of ML: optimizing a objective function over a large class for the purposes of prediction or classification (in this case, we are predicting the best policy). A very short introduction to ML can be found in Section 5.1.

# 2.5.2 Temporal Differences

Where do we find a critic? how can we estimate a value function without a model? One answer lies in the sample representation of the fixed dynamic programming equation, previously announced in (2.30). For any $	heta$, the fixed

```
$J_	heta(x(k)) = c(x(k),u(k)) + J_	heta(x(k+1)), \quad k \geq 0, \quad u(k) = \phi^	heta(x(k)).$$
```

We might seek an approximation $\hat{J}$ for this identity is well approximated. This motivates the *temporal difference* (TD) sequence used in RL algorithms:

```
$$\mathcal{D}_{k+1}(\hat{J}) = -\hat{J}(x(k)) + \hat{J}(x(k+1)) + c(x(k),u(k)), \quad k \geq 0, \quad u(k) = \phi^	heta(x(k)).$$
```