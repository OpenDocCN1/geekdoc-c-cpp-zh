
# Temporal Difference Methods

The analysis that follows concludes with Proposition 9.27, which implies that the condition number for the linearized ODE dynamics can be expected to be of order $O(1/(1-\gamma)^2)$. Consequently, GQ learning is probably not the best option in a tabular setting. It is presented here may be useful in function approximation settings where it is not known if $f^0(\theta)=0$ has a solution.

# GQ Analysis

The fast time-scale recursion (9.9ab) is designed so that $\omega_n \approx Mf^0(\theta_n)$ for large $n$. Theory for two-scale SA provides an approximation of (9.94a):

$$\theta_{n+1} \approx \theta_n + \alpha_{n+1}\{\mathcal{D}_n + \zeta_n - \gamma f^0(\theta_n)^\top M\zeta_n\psi_{(n+1)}\}$$

We conclude that the ODE: approximation of this recursion is gradient descent on applying Lemma 9.26 and (9.93). The course of condition number is potentially worse when using this algorithm:

**Proposition 9.27** *Suppose that the optimal policy $\phi^*$ is unique. Then the linearization matrix for GQ-learning is given*

$$A_{GQ} = -\nabla^2\Gamma(\theta^*) = -[I - \gamma T^*]\Pi[I - \gamma T^*]$$

Consequently, the eigenvalues of the matrix $A_{GQ}$ are real and nonpositive, and its condition number admits the lower bound

$$\kappa(A_{GQ}) \geq \frac{d}{(1-\gamma)^2}\{\max((1-\lambda)^2v^\top\Pi v)\}$$

where the max is over all eigenvalue-eigenvector pairs $(\lambda, v)$ for $T^*$ satisfying $||v||=1$.

*Proof* $A_{GQ} = -\nabla^2\Gamma(\theta^*)$ is symmetric, and its condition number is the ratio of eigenvalues:

$$\kappa(A_{GQ}) = \frac{\lambda_{max}(\nabla^2\Gamma(\theta^*))}{\lambda_{min}(\nabla^2\Gamma(\theta^*))}$$

It remains to establish the following bounds:

$$\lambda_{min}(\nabla^2\Gamma(\theta^*)) \leq (1-\gamma)^2v^\top\Pi v, \text{ for any eigenvalue-eigenvector pair $(\lambda, v) \text{ for } T^*,$$

$$\lambda_{max}(\nabla^2\Gamma(\theta^*)) \geq (1-\lambda)^2v^\top\Pi v.$$

where in (9.95b) the eigenvectors are normalized, with $||v||=1$.

The proof is based on the pair of inequalities:

$$\lambda_{min}(\nabla^2\Gamma(\theta^*)) = \min v^\top\nabla^2\Gamma(\theta^*)v$$
$$\lambda_{max}(\nabla^2\Gamma(\theta^*)) = \max v^\top\nabla^2\Gamma(\theta^*)v$$

where the max and min are over all $v \in \mathbb{R}^d$ satisfying $||v||=1$. To obtain bounds, we restrict to eigenvectors of $T^*$ particular $||v||=1$, from which we obtain

$$v^\top\nabla^2\Gamma(\theta^*)v = v^\top[I - \gamma T^*]\Pi[I - \gamma T^*]v = (1-\lambda)^2v^\top\Pi v$$

# 9.8 GQ and Zap

and hence the pair of bounds:

$$\lambda_{\min}(\nabla^2\Gamma(\theta^*)) \le (1-\lambda^*)^2v^\top\Pi v \le \lambda_{\max}(\nabla^2\Gamma(\theta^*))$$

The lower bound (9.95b) follows. To obtain the bound (9.95a) on the minimal eigenvector, take $v=1/\sqrt{d}$, which is an eigenvector of $T^*$ with eigenvalue $\lambda=1$:

$$\lambda_{\min}(\nabla^2\Gamma(\theta^*)) \le (1-\lambda^*)^2v^\top\Pi v = (1-\gamma^*)^2/d.$$

# 9.8 Zap

To crush the condition number, there is no better approach than SA. This is easily adapted to Q-learning, even in function approximation settings. For analysis, we continue to restrict to tabular setting. The quadratic SA representation of Watkins's algorithm in (9.7) is most easily adapted to create algorithm.

# 9.8 Q-Learning

For initialization $\theta_0 \in \mathbb{R}^d$ and $\tilde{A}_0 \in \mathbb{R}^{d \times d}$, with $\{A_n, b_n\}$ defined in (9.7),

$$\tilde{A}_{n+1} = \tilde{A}_n + \beta_{n+1}\{-\tilde{A}_n+b_{n+1}\}$$
$$\theta_{n+1}=\theta_n+\alpha_{n+1}G_n[A_{n+1}-b_{n+1}], \quad G_{n+1}=-\tilde{A}_{n+1}^{-1}$$

where the two-step sequences satisfy (8.22). This algorithm is intended to approximate Newton-Raphson flow:

$$\frac{d}{dt}\theta(t) = G(\theta)f^0(\theta)$$

With $G(\theta) = [-\partial_\theta f^0(\theta)]^{-1}$. Based on representation for $f^0$ in (9.2) Lemma 9.25, which gives $A(\theta)$, and using the suitable notation $q_t$ in place of $\theta_t$, this becomes

$$\frac{d}{dt}q_t = -q_t - A(q_t)^{-1}b, \quad q_t \in \Theta^m$$

On denoting $\tilde{q}_t=q_t-q^m$, we obtain linear dynamics in $\Theta^m$:

$$\frac{d}{dt}\tilde{q}_t^m = -\tilde{q}_t^m \quad m=3.$$

These dynamics are illustrated in Figure 9.4 with $m=3$. Testing the Zap Q-learning with asymptotic covariance, given by (8.30):

$$\Sigma^* = A^{-1}\Sigma_{\Delta}(A^{-1})^T.$$

# Temporal Difference Methods

![img/0790f102daffa7564329bf76cd0815_369_0.png]

**Figure 9.5** Comparison of theoretical and empirical variance for Q-learning applied to six-state example. Row 1: Watkins's algorithm with $g=7,\gamma=0.8$. Row 2: Q-learning with $\gamma=0.8$. Row 3: Q-learning with $\gamma=0.99$.

For illustration, consider the six-state example shown in Figure 9.1 for which it is possible to compute $A$ and $\Sigma_{\Delta}$. With $M=10^3$ independent runs, histograms of the normalized error are obtained:

$$W_n = \sqrt{|\theta_n - \bar{\theta}_n|}, \quad \hat{\theta}_n = \frac{1}{M} \sum_{i=1}^M \theta_i^n. \quad (9.98)$$

Figure 1.1 shows a sample path of Q-learning, compared with other algorithms using step-size $\alpha_n=1/n$ (a poor choice, since in this plot the discount factor was $\gamma=0.99$).

Figure 9.5 shows histograms obtained using Zap Q-learning, and also Watkins's algorithm using step-size $\alpha_n=g/n$ with $g=7$ (resulting in finite covariance for the discount factor $\gamma=0.8$).

The first row shows the histogram for Watkins's algorithm, and the second and third rows for Zap Q-learning, with $\beta_n=(\alpha_n)^{0.85}=1/n^{0.85}$. Data in the third row were observed with the discount factor $\gamma=0.99$. The covariance estimates and the Gaussian approximations match the theoretical predictions for $n\ge10$.

Analysis of this algorithm falls outside the scope of this book because $A(\theta)$ is not continuous, so there is no "off the shelf" theory to justify an ODE approximation. Exploiting concavity of the entries of $f^0$, it is possible to justify an ODE approximation, and this can be extended to generalized nonlinear function approximation (with substantial effort).

# Zap

Zap Q-learning is fast in practice, but the update equation for $\theta_{n+1}$ in (9.96) is complex. We have a solution to this complexity using the first-order SA algorithm (8.52). The algorithm is applicable because one crucial assumption of the Projection holds: $A(\theta)$ is Hurwitz for each $\theta$. With $\{A_n, b_n\}$ defined in (9.7), the algorithm (8.52) is expressed as follows:

# 9.9 Technical Proofs

![img/0790f102daffa7564329bf76cd0815_370_0.png]

**Figure 9.6** Span norm error for Zap Zero Q-learning.

## Zap Zero Q-Learning

Initialize $\theta_0, \omega_0 \in \mathbb{R}^d$, Update for $n \geq 0$:

$$\theta_{n+1} = \theta_n + c_n\omega_n,$$
$$\omega_{n+1} = \omega_n + \beta_n + \beta_{n+1}\{A_{n+1}\theta_n - b_{n+1}\}$$

the following two-step sequences satisfy (8.22). The fast time-scale recursion (9.9b) is designed to obtain the approximation:

$$\omega_{n} \approx -A(\theta_n)^{-1}\{A(\theta_n)\theta_n - b\}$$

The Zap Zero algorithm is not much better than Watkins's original algorithm. We have doubled the number of parameter elements since we must update $\theta_n$ and $\omega_n$ at each stage, but the updates are not all complex.

When this and Zap Q-learning are compared for the example considered in Figure 9.3 we observe that the span errors for the respective parameter estimates $\{\theta_n\}$ are very similar. Results are shown in Figure 9.6, alongside results using PJR averaging and Watkins's algorithm with gain $g = 1/(1-\gamma)$. The transient behavior of Zap Zero Q-learning is better than what is obtained using averaging, and a bit worse than Zap Q-learning. For Zap Q-learning, any value $0.6 \leq \rho \leq 0.9$ for $\beta_n = n^{-\rho}$ in (9.96) gives performance. However, for Zap Zero and PJR averaging, was found in this example that a large step-size $\rho$ is required for the time scale. These results were obtained using $\beta_n = n^{-\rho}$ with $\rho = 0.1$. Performance was terrible for Zap Zero and PJR averaging with $\rho \geq 0.5$. New theory is needed to explain these findings.

### 9.9.1 Advantage Function

Proof of Proposition 9.1 The conclusion $G^*(x) = E[Q(\phi(n)) | X(n) = x] = \sum_{u} \phi(u) | x)Q(x,u) = \underline{Q}(x)$ is obtained upon recalling the definition of the conditional expectation in (9.15).
