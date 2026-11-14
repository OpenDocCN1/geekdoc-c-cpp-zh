

Note that

$(u_* - \psi)^-(u_* - l - \alpha \Phi u_*) = 0.$

We can pass to the limit and obtain

$(u^* - \psi)^-(u^* - l - \alpha \Phi u^*) = 0.$

Using the property $u^* - \psi \le 0$, we can also write

$(u^* - \psi)(u^* - l - \alpha \Phi u^*) = 0,$

which implies that $u^*$ is a solution of (7.3.2). The proof has been completed. $\square$

## 7.4. ERGODIC CASE

We study now the ergodic problem, letting $\alpha \to 1$.

### 7.4.1. SETTING OF THE MODEL.

We shall make here the assumptions of Theorem 7.1 and also

(7.4.1) \( l, \psi \ge 0, \text{bounded}, l(x) \ge l_0 > 0. \)

We consider the problem

(7.4.2) \( u_\alpha(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \alpha \Phi^* u_\alpha(x)] \right\}, \forall x. \)

We know that it has a unique l.s.c. continuous solution (by contraction mapping arguments).

The issue is to study the limit of $u_\alpha$ as $\alpha$ tends to 1. In fact this problem will be easier than the one without the obstacle $\psi$. The reason is because the function $u_\alpha$ will remain bounded.

### 7.4.2. THE MAIN RESULT.

We state the main result

#### Theorem 7.4.

We make the assumptions of Theorem 7.1 and (7.4.1). Consider the equation

(7.4.3) \( u(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \Phi^* u(x)] \right\}, \forall x, \)

then it has a positive bounded l.s.c. solution which is unique. Moreover \( u_\alpha(x) \uparrow u(x) \) as \( \alpha \uparrow 1 \).

#### PROOF.

We prove the existence and uniqueness of the solution $z$. We cannot use the argument of contraction mapping, since $\alpha = 1$. To prove the existence of a positive bounded l.s.c. solution, we consider the increasing sequence

u_0 = 0

u_{n+1}(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \Phi^* u_n(x)] \right\}

then clearly

u_0 \le u_1 \cdots \le u_n \le \cdots \psi,

hence \( u_n \uparrow u \ge 0 \). Moreover \( u \le \psi \) and is l.s.c.

Reasoning as in the proof of Theorem 7.1 we check that the limit $u$ has the desired properties and is a solution. Let us prove the uniqueness of a Borel bounded solution. We cannot use the contraction mapping argument. We use the following trick. We first exclude the case $\psi = 0$ in which case the unique solution is $u = 0$.

Suppose there exist two positive bounded solutions \(z_1, z_2\). Suppose there exists a point \(x^*\) such that \(z_2(x^*) < z_1(x^*)\). Then we have

$$\gamma = \inf_{\{x|z_1(x)>0\}} \frac{z_2(x)}{z_1(x)} < 1.$$

We are going to show a contradiction. We are going to construct a number \(\beta\) with \(\gamma < \beta \le 1\) such that \(\beta z_1(x) \le z_2(x), \forall x\). It will follow

$$\gamma = \inf_{\{x|z_1(x)>0\}} \frac{z_2(x)}{z_1(x)} \ge \beta,$$

which is a contradiction.

Let \(0 < \lambda < 1\). A solution \(z\) satisfies also

$$z(x) = \min \left\{ \lambda \psi(x) + (1-\lambda)z(x), \inf_{v \in U} [l(x,v) + (1-\lambda)z(x) + \lambda \Phi^v z(x)] \right\}.$$

This is in particular satisfied with \(z_1\) and \(z_2\). Note that

$$\beta z_1(x) = \min \left\{ \beta \lambda \psi(x) + (1-\lambda)\beta z_1(x), \inf_{v \in U} [\beta l(x,v) + (1-\lambda)\beta z_1(x) + \lambda \Phi^v \beta z_1(x)] \right\}.$$

One could claim that \(\beta z_1(x) \le z_2(x)\) whenever

$$\beta \lambda \psi(x) + (1-\lambda)\beta z_1(x) \le \lambda \psi(x) + (1-\lambda)z_2(x)$$
$$\lambda l(x,v) + (1-\lambda)\beta z_1(x) \le l(x,v) + (1-\lambda)z_2(x)$$

Since \(z_2(x) \ge \gamma z_1(x)\), it is sufficient to guarantee that

$$\beta \lambda \psi(x) + (1-\lambda)\beta z_1(x) \le \lambda \psi(x) + (1-\lambda)\gamma z_1(x)$$
$$\lambda l(x,v) + (1-\lambda)\beta z_1(x) \le l(x,v) + (1-\lambda)\gamma z_1(x)$$

We must have

$$(1-\lambda)(\beta-\gamma)z_1(x) \le \lambda(1-\beta)\psi(x)$$
$$(1-\lambda)(\beta-\gamma)z_1(x) \le \lambda(1-\beta)l(x,v)$$

It is sufficient to check that

$$(1-\lambda)(\beta-\gamma) \le \lambda(1-\beta)$$
$$(1-\lambda)(\beta-\gamma) \le \lambda(1-\beta) \frac{l_0}{\|\psi\|}$$

It is sufficient to choose \(\beta\) such that

$$\frac{\beta-\gamma}{1-\beta} = \rho = \frac{\lambda}{1-\lambda} \min \left( 1, \frac{l_0}{\|\psi\|} \right),$$

hence

$$\beta = \frac{\rho+\gamma}{1+\rho}.$$

and \(\gamma < \beta \le 1\). The contradiction has been established. From this contradiction it follows that \(z_2(x) \ge z_1(x), \forall x\). By symmetry between \(z_1\) and \(z_2\) we obtain \(z_1 = z_2\). The uniqueness has then been proven.

To complete the proof, we have to check the convergence property. We first prove that

$$\alpha \le \alpha' \Rightarrow u_\alpha \le u_{\alpha'}.$$

This property is obtained by considering the increasing sequence

$$u_{\alpha, n+1}(x) = \min \left\{ \psi(x), \inf_{v} [l(x,v) + \alpha \Phi^v u_{\alpha,n}(x)] \right\}$$

and \(u_{\alpha,0}(x) = 0\). It is clear that

$$u_{\alpha,n}(x) \le u_{\alpha',n}(x) \to u_{\alpha,n+1}(x) \le u_{\alpha',n+1}(x),$$

and the monotonicity result follows.

We next write

$$u_\alpha(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x,v) + \Phi^v u_\alpha(x) - (1-\alpha)\Phi^v u_\alpha(x)] \right\}, \forall x.$$

Since \(||(1-\alpha)\Phi^v u_\alpha|| \le (1-\alpha)||u_\alpha||\), hence tends to 0, we see easily that \(u_\alpha \uparrow u^*\) which is the solution of (7.4.3). The proof has been completed.

**Remark.** If the functions \(l(x,v)\) and \(\psi\) are continuous then the solution of (7.4.3) is also continuous. This is checked by defining a monotone decreasing sequence, converging towards a solution, which is u.s.c. By uniqueness, the solution is continuous.

### 7.4.3. PROBABILISTIC INTERPRETATION.

We consider as in section 7.2, a decision rule \(V\) and a stopping time \(\theta\). We then define the pay-off

$$J_x(V, \theta) = E^{V,x} \left[ \sum_{j=1}^{\theta-1} l(y_j, v_j) + \psi(y_\theta) \mathbf{1}_{\theta < \infty} \right].$$

We can state the

#### Theorem 7.5.

We make the assumptions of Theorem 7.4. We then have

$$u(x) = \inf_{V, \theta} J_x(V, \theta).$$

Proof. We first remark that

$$\psi(x) \ge J_x(V, \theta) \ge l_0 E^{V,x}(\theta - 1),$$

so, without any restriction, we can assume that \(\theta < \infty\) a.s. \(P^{V,x}\). One then checks the inequality

$$u(x) \le E^{V,x} \left[ \sum_{j=1}^{\theta-1} l(y_j, v_j) + u(y_\theta) \right] \le J_x(V, \theta).$$

Define next the feedback \(\tilde{v}(x)\) Borel function with values in \(U\) which attains the infimum in \(v\) in equation (7.4.3). We then define

$$\tilde{\theta} = \inf \{ n \ge 1 | u(y_n) = \psi(y_n) \}.$$

We can assert that

$$E^{V,x}[\tilde{\theta}] \le \frac{\psi(x)}{l_0}.$$

Indeed, for any \(N\) we can write

$$u(x) = E^{V,x} \left[ \sum_{j=1}^{\tilde{\theta} \wedge N - 1} l(y_j, v_j) + u(y_{\tilde{\theta} \wedge N}) \right] \ge l_0 E^{V,x} \tilde{\theta} \wedge N.$$

Since \(u(x) \le \psi(x)\) we also obtain

$$E^{\tilde{V},x}[\tilde{\theta} \wedge N] \le \frac{\psi(x)}{l_0}$$

and letting \(N\) go to \(\infty\) the desired estimate is obtained. We therefore can write

$$u(x) = E^{\tilde{V}, x} \left[ \sum_{j=1}^{\tilde{\theta}-1} l(y_j, v_j) + u(y_{\tilde{\theta}}) \right]$$

Also \(u(y_{\tilde{\theta}}) = \psi(y_{\tilde{\theta}})\) since \(\tilde{\theta} < \infty\) a.s. \(P^{\tilde{V}, x}\). Therefore

$$u(x) = J_x(V, \tilde{\theta})$$

and the proof has been completed.

**Exercise 7.8.** Check that when \(l_0 = 0\), \(u_n \uparrow\) minimum solution of equation (7.4.3). This minimum solution is the value function defined in the statement of Theorem 7.5.

This page intentionally left blank

## IMPULSE CONTROL

Impulse Control has been studied mainly in continuous time, see [8]. Indeed, in continuous time the difference between an impulse control and a continuous control is quite apparent. An impulse control allows for jumps on the state of the system. A continuous control allows only for a continuous evolution of the state of the system and forbids jumps. In discrete time, there is of course no continuous evolution, so it looks as if the concept looses its specificity; the state at time n+1 can be considered as a jump from the state at time n. However, we will identify an analogy with optimal stopping. One can embed optimal stopping into a standard control problem in discrete time, but one can also treat it in a specific way. Similarly, an impulse control problem can be embedded into a standard control problem in discrete time, but one can also consider it in a specific manner. In that case it will look like optimal stopping, but with a sequence of stopping times instead of a single stopping time. We will begin by describing the model. Then we introduce the basic tool, which is the functional equation arising from Dynamic Programming. We study it directly by analytic techniques. We finally proceed with the interpretation.

### 8.1. DESCRIPTION OF THE MODEL

#### 8.1.1. TRANSITION PROBABILITY.

In this set up we will consider a controlled Markov chain with special features. It is at the same time a generalization and a special case of the general framework. However, we shall need the fact that X is a vector space or a subspace of a vector space. To fix the ideas we take X = R^d or X = (R^d)^+. We consider as usual a transition probability \pi(x, v, d\eta). We define then the transition probability

$$\pi(x, v, w, d\eta) = \pi(x + v, w, d\eta).$$

It is indeed a generalization of the usual case, which is recovered by fixing the value w = 0, but also a particular case, considering the pair v, w as a control. We associate to the transition probability the operator

$$\Phi^{v,w} f(x) = \int_{R^d} f(\eta) \pi(x, v, w, d\eta).$$

Considering the operator $\Phi^v$ associated to $\pi(x, v, d\eta)$ we have obviously

$$\Phi^{v,w} f(x) = \Phi^v f(x + w).$$

The controls v, w are mathematically similar, but in practice act differently. The control v modifies the transition probability, but does not change x. The control w modifies x. Its influence is instantaneous, instead of taking place at the next period. This is why it is called an impulse. So the difference remains meaningful, even though we are in discrete time. We remark also that if the assumption (4.3.1) is satisfied for $\Phi^{v,w}$, it carries over to $\Phi^{v,w}$.

