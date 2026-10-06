# 9.11 Notes

$f_{n+1}(	heta) - f_{n+1}(	heta_n)\}_i \le \sum A_{n+1}(i,j)|	heta(j) - 	heta_n(j)|, \quad 1 \le i \le d, \quad \theta \in \mathbb{R}^d.$

This holds for the algorithm (9.76) with linear function approximation, provided the basis vector has non-negative entries, $\psi; X \times U \to \mathbb{R}^d$. It is not difficult to show that a similar inequality is preserved in any ODE limit, which is all that is needed to show that $V(\theta) \equiv |\f^0(\theta)\|^2$ serves as a Lyapunov function for the SA algorithm.

Relaxing the positivity assumption was a bigger challenge than confronting a nonlinear function approximation architecture.

The article [90] also contains many numerical examples illustrating the application of Zap Q-learning with neural network function approximation.

# 9.11.4 Convex Q-Learning

Extensions of the convex Q algorithms of Section 5.5 are described in [246, 247]. The main challenge in algorithm design is that the constraints involve a conditional expectation. For example, (5.63) would be modified as follows:

```
$$\max_{\theta} \langle\mu, H^\theta\rangle \ns.t. H^\theta(x,u) \le c(x,u) + E[H^\theta(\Phi(k+1)) | \Phi(k) = (x,u)], \quad x \in X, u \in U(x).$
(9.106)
```

The conditional expectation can be approximated to obtain an algorithm, as discussed in Section 9.2. The use of **experience replay** is another approach based on empirical distributions (see [338, ch. 16] and [211]). Theory for convex Q-learning remains immature, best left to a sequel or second edition.

The recent paper [218] is based on a variant of the convex program (9.106) in the tabular setting, and [224] contains an algorithm very similar to convex Q-learning (see [224, (6)]). The more recent RL survey [269] has a version of convex Q-learning, and explains the importance of regularization. Also related to (9.106) is the *logistic Q-learning* algorithm of [28], which may represent an opening for more practical algorithms, as well as more elegant theory.