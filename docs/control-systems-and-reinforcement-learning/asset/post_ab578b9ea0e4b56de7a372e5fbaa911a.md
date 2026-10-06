
## 388 Setting the Stage, Return of the Actors

Next apply Lemma 10.24 (i) using $H = \psi_i$, for arbitrary $i$. Letting $A^i$ denote the $i$th column of $A$, the lemma implies

```
$A^i = \mathbb{E}[\{\psi_i(\Phi(0)) + \gamma^i\{\Phi(n+1) \neq z^i\}\psi_i(\Phi(n+1))}\zeta_n]$
$A^i = \mathbb{E}[\{\psi_i(\Phi(0))\psi(\Phi(0))}]$
```

This establishes part (i); $A = R^{\theta}$. For (ii), the first-order condition for optimality for a parameter $\theta^0 \in \mathbb{R}^d$;

```
$0 = \nabla_{\theta} \mathbb{E}[\{(H^{\theta}(\Phi(n)) - J_{\theta}(\Phi(n)))^2]_{\theta=\theta^0} = \mathbb{E}[\{(H^{\theta^0}(\Phi(n)) - J_{\theta}(\Phi(n)))\psi_n\}]$.
```

By definition, $\mathbb{E}[H^{\theta}(\Phi(n))\psi_n] = R(\theta^0) = -A^{\theta^0}$. Applying Lemma 10.23,

```
$-mathbb{E}[J_{\theta}(\Phi(n))\psi_n] = -\mathbb{E}[c_{n,b}] = b,
```

$b = \mathbb{E}[b_{n+1}]$ (see (10.21)). Hence the first-order condition for optimality becomes
$-A^{\theta^0} + b=0$ as claimed.

Proof of Theorem 10.15: We first establish that $\eta = \delta\langle\mu, H^{\theta}\rangle$ for any function of $f(0)=0$. For this theorem, we take $g(z) = c(z) - \delta\langle\mu, H^{\theta}\rangle$ and apply Lemma 10.24 (ii):

```
$0 = \bar{f}(\theta^0) = \mathbb{E}[\{g(\Phi(n)) - H^{\theta}(\Phi(n)) + H^{\theta}(\Phi(n+1))}\zeta_n]_{\theta=\theta^0},$
$0 = \mathbb{E}[\{g(\Phi(0)) - H^{\theta}(\Phi(0)) + H^{\theta}\psi(\Phi(0))\}]. (10.57)
```

where

```
$\tilde{g}(z) = \mathbb{E}[\{\sum_{k=0}^{-1} [c(\Phi(k)) - \delta\langle\mu, H^{\theta}\rangle | \Phi(0) = z]]$
```

We use the special property of

```
$0 = \sum_{i} f_i^{\theta^0}(z^*) = \sum_{i} \theta_i^0 \mathbb{E}[\{\psi_i(\Phi(0))\{\tilde{g}(\Phi(0)) - H^{\theta^0}(\Phi(0)) + H^{\theta^0}(z^*)\}]$
$0 = \mathbb{E}[\{\Phi(0) = z^*\{\tilde{g}(\Phi(0)) - H^{\theta^0}(\Phi(0)) + H^{\theta^0}(z^*)\}\}].
```

```
$0 = \mathbb{E}[\{\Phi(0) = z^*\{\tilde{g}(\Phi(0)) - H^{\theta^0}(\Phi(0)) + H^{\theta^0}(z^*)\}\}]$
= \mathbb{E}[\{z^*{\tilde{g}(z^*)\}].
```

Under the assumptions of the theorem, it follows that $\tilde{g}(z^*) = 0$ and hence $\eta = \delta\langle\mu, H^{\theta^0}\rangle$
By Proposition 6.1 (Kac theorem), which is (i).
We also conclude that $\tilde{g} = H_3$, so that (10.57) implies (ii).

The remainder of the proof follows the proof of Theorem 10.11. First, revisiting the (10.57) with the knowledge that $\tilde{g} = \tilde{c}$,

```
$0 = \mathbb{E}[\{(H^{\theta^*}(\Phi(0)) - r^* - H_3(\Phi(0))}\psi(\Phi(0))\}] (10.58)
```

with $r^* = H^{\theta^*}(z^*)$. We now show that this equation characterizes optimality of (10.34). The first-order condition of optimality for $(\theta^0, r^0) \in \mathbb{R}^{d+1}$ for the minimization in (10.34) is

```
$0 = \mathbb{E}[\{(H^{\theta^*}(\Phi(0)) - r^* - H_3(\Phi(0))}\psi(\Phi(0))\}]$
$0 = \mathbb{E}[\{(H^{\theta^*}(\Phi(0)) - r^* - H_3(\Phi(0))\}].
```

## 10.10 Notes

The first equation is obtained by taking the gradient with respect to $\theta$, and the second by taking the derivative with respect to $r$. The second equation follows from the first under the assumption that 1 is in the span of $\{\psi_i\}$. Hence (10.58) implies that $(\theta^*, r^*)$ satisfies the first-order optimality condition.

## 10.1.1 Adjoints and TD-Learning

Most of this theory in this chapter was developed by the MIT group led by John Tsitslis in a single decade starting in the early 1990s. The wonderful geometry surrounding TD learning is part of the development of Roy [363], which summarizes several remarkable papers, including [353–356]. Proposition 10.1 appears as [356, Theorem 1], with bounds for any value of $\lambda$: with $\theta^*(\lambda)$ the solution to TD$(\lambda$),

```
||H^{\theta^*}(\lambda) - Q||_\alpha^2 \le \frac{1-\lambda}{1-\gamma} ||Q||_\alpha^2, \quad \tilde{Q} = H^{\theta^*}(1).
```

The use of regeneration to define the eligibility sequence (10.19), inspired by the older representation of Poisson's equation $H_3$ in (10.17), was introduced in [192] upon realizing that TD(1) could be used to obtain unbiased gradient estimates. Sutton's monograph [277] had great impact in both statistics and Markov chain theory. His significant contribution, highlighted in his book, is regeneration times can be constructed for a Markov chain on a continuous state space. This may be valuable in future research.

## 10.2 Actor-Critic Methods

Glynn's research in the 1980s [142, 143] introduced likelihood ratio methods for stochastic descent without bias, based in part [313] (i.e., sensitivity surveyed in Section 6.8). One decade later, this was extended and applied to obtain the first unbiased stochastic descent approach for reinforcement learning [238, 239] (see also [31, 321]), followed soon after with new insights in [344]. This was the start of the late nineties actor-critic revolution.

Two time-scale approximation and variance was still evolving in the late 1990s. Konda's work with Borkar [189, 190] and then Tsitsiklis [188, 193] helped to shed light on this topic, and [188, 192] introduced a major advancement in actor-critic theory and application: the computable features property (10.47) was introduced in this work, based on the $L_2$ theory surveyed over [353–356]. The introduction of the advantage function as a method to accelerate actor-critic algorithms was proposed in [172], following [238]. This was later applied to obtain the trust region policy optimization (TRPO) algorithm of which spawned many other approaches. The regenerative structure leading to the i.i.d. samples $\{S_n\}$ in (10.24) suggests that the policy should be frozen between regeneration times in algorithm implementation,

Setting the Stage, Return of the Actors

similar to the way qSGD was applied for the mountain car example in Section 4.7.1. This was one approach in [238, 239], and similar “episodic” approaches are used in [311, 312]. The better advantage control technique is new, along with concave comparison Position 10.22. The natural actor critic algorithm was introduced in [173] (see also [53, 56, 151, 285]). The value of the natural gradient in terms of acceleration is explained in [2]; also, in this work and the current research [48, 248] it is shown that a large class of policy gradient algorithms are globally convergent with appropriate regularization (reg $R\theta$), discussed after (10.46). The recent article [368] provides an elegant Lyapunov analysis for bandit problems, and [236] contain a survey of actor-critic methods. Absent from this chapter is any discussion on how to choose the regularizer in (10.46) for application to gradient descent. [270] for an approach intended to improve both policy and value function optimization. Left out of this chapter is any mention of the application of the gradient-free techniques emphasized in Sections 4.6 and 7 based on PPSA – a history can be found in Section 4.11. Williams’s REINFORCE algorithm [376] may be the first to apply these techniques to MDPs to create actor-only algorithms of the form described in Section 4.6. More recently, in [236] it is argued that PPSA is sometimes more efficient than any method. Algorithm 1 of [236] is a version of PPSA, and essentially the same as the original Kiefer-Wolowitz algorithm [182]. However, the efficiency results of [236] deserve a warning label: *Any technique involving multiple evaluations for a single gradient estimate must take into account observation noise.* This concern is the reason for emphasis on qSGD methods #1 and #2 in Section 4.6 of this book.

## 10.10 Some Ancient History

Many in the RL community have lost track of the ancient control theory for Markov chains pioneered by Mann [235] and Borkar [60–62]. This work is easy to miss—the language and notation is so different from what is used today in the RL literature. The authors begin with a family of transition matrices $T(\theta : \theta \in \mathbb{R}^d)$ and in later, the theory is extended to general state spaces and continuous time. One goal is to find the parameter $\theta^*$ that minimizes the average cost. A reader might dismiss this as being from RL, since the family of models is assumed known. A closer look reveals that the observations are log-likelihoods, $L_{\theta} = \log(T_{\theta}/T_{\theta^0})$, where $\theta^0$ is fixed but auxiliary (it plays no essential role in the theory). The setting is thus far more general than this. The very special case (10.37).

```
$L_{\theta}(z,z') = \log \frac{\phi^{\theta}(u'|x')}{\phi^{\theta^0}(u'|x')} \quad z, z' = (x',u') \in Z$.
```

This “ancient history” deserves closer inspection, as well as the substantial concurrent work in the USSR [136].
