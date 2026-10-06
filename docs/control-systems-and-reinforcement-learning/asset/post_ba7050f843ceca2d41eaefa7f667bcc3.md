
## 2.2 What to Do about It?

1) Nearly invariant response was provided at essentially all aerodynamic flight conditions 2) accurate priori knowledge of aircraft aerodynamic characteristics was not required to design a satisfactory system 3) aircraft configuration changes were adequately compensated for 4) The redundant control provided a reliable and fail-safe system.

It was also noted that the adaptive control system “inspired confidence and allowed the pilot to spend time cross-checking flight instruments, checking subsystems, ‘sight-seeing.”

These observations followed 65 test flights. The control system was not robust enough to provide stable control in all situations encountered. Sadly, a pilot died in a crash attributed to oscillations induced by the adaptive system. The research program was shut down, but the tragedy inspired greater attention to robustness in control design.

> It should go without saying that every control engineer or practicing economist must study failures. Airplanes and economies inevitably crash. In the long run, it is a greater tragedy if the experts do not both learn from disaster.

## 2.2 What to Do about It?

The vast literature on control solutions is built upon a measure of input–output behavior that is used to design the policy $\phi$. Modeling and control design are each art form, with possible solutions from vast statistics and control tools.

When we say, a sequence of mappings from inputs to outputs:
$y(k) = G_{\phi}(u(0), u(1), \dots, u(k)), \quad k \ge 0.$ (2.2)

The functions of $G_{\phi}$ may also depend on exogenous variables (outside our control), such as weather and traffic. And here come one of the most vital principles of control design: the model must capture essential properties of the system to be controlled, and simultaneously simple enough to be useful. For example, aerospace engineers will create models for the design of flight controls and from this a policy $\phi$ designed to work for. Of course, they do not. The next step is to create entirely new model for validation and simulate a range of scenarios: What happens when the plane is full, empty? How does the control system perform when an engine fails? If one of these tests fails, then the control engineer gains to improve the model, or additional sensors to measure pitch angles, or more powerful motors to control ailerons, flaps, or elevators. I am writing general principles for anyone interested in control:

(1) Create a model for control.
(2) Design the policy $\phi$ based on the model.
(3) Simulate based on high-fidelity model, and then revisit 1 and 2.

The success of this approach has been tremendous, as seen in history [15].

### Linear Time Invariant Model

The most successful class of models are linear and time invariant (LTI). The general LTI model is defined by a sequence of scalars $\{b_i\}$ (impulse response), and for a scalar input $u$, the model defines $y(k)$ as the sum
$y(k) = \sum_{i=0}^{k} b_i u(k-i), \quad k \geq 0.$

This is in fact complex in many situations. A more tractable subclass of LTI models are autoregressive moving-average (ARMA): for scalar coefficients $\{a_i, b_i\}$,
$y(k) = -\sum_{i=1}^{N} a_i y(k-i) + \sum_{i=0}^{M} b_i u(k-i), \quad k \geq 0.$

A linear input-output model motivates the design of a policy $\phi$ that has a similar linear form. A common design technique based on optimization will be described in the following chapters, beginning in Section 3.6.

## 2.3 State Space Models

### 2.3.1 Sufficient Statistics and Nonlinear State Space Model

In statistics, the term sufficient statistic is used to denote a quantity that summarizes all past observations. The state plays an analogous role in control theory. A state space model requires the following ingredients: the state space $X$ on which the state $x$ evolves, and an input space (or action space) on which the input $u$ evolves. We may have additional constraints coupling the state and the input, which is modeled via
$u(k) \in U(x), \quad \text{when } x \in X,$ with $u(x) \subseteq U$ for each $x$. We might want to model an observation process $y$ evolving on a set $Y$. In the control theory literature, it is common to assume that $X, U$, and $Y$ are subsets of Euclidean space, while in operations research and reinforcement learning it is more common to assume these are finite sets. However, in this book we prefer the control perspective that we can more easily search for structure of control solutions: for example, an optimal input a continuous function of the state?

We require two functions $F: X \times U \to X$ and $G: X \times U \to Y$ that define the state equations:
$x(k+1) = F(x(k), u(k)), \quad x(0) = x_0,$
$y(k) = G(x(k), u(k)).$

An LTI model can be transformed into a state space model in which the two functions $F, G$ are linear in $(x, u)$. We might allow $F, G$ to depend upon the time variable $k$. It is argued in Section 3.3 that it is often more convenient to assume that the state $x(k)$ includes $k$ as one component.

### 2.3 State Models

However, there is one example of a time-dependent model that highlights the role of state as a sufficient statistic. The input-output model (2.2) always has a state space description, in which the state is the history of the following inputs:
$x(k+1) = [u(0), u(1), u(2), \dots, u(k)]^T$

We have $x(k+1) = F_k(x(k), u(k))$, denoted by concatenation, and $y(k) = G_k(x(k), u(k))$ is a restatement of. In this dynamic model in which history fully determines the output, (2.7) is called the (full) history. A practical state space can be regarded as a compression of the history state.$^3$

In many cases, we can construct a good policy via state feedback, $u(k) = \Phi(x(k))$, for some $\Phi: \mathbb{R}^* \to \mathbb{R}$; in stochastic control, it is typical to say that $\Phi$ is a Markov policy in this case. however, the power of this approach is fully realized if we are flexible in our definition of the state. We won't be using the full history because of complexity; what's more, the "full history" may not be rich enough.

### 2.3.2 State Augmentation and Learning

Tracking and disturbance are not sacred; state augmentation simplifies to control design. Here we provide a brief glimpse of tricks used to simultaneously track the reference $r$ while rejecting disturbances:

- (i) The definition of state is not sacred; state augmentation simplifies control design.
- (ii) Unknown quantities, including disturbances and even the state space model, can be learned based on input-output measurements.

Let's make our simplifying assumption that the input and output are scalar valued, and take $X = \mathbb{R}^n$. The state evolution is also influenced by a scalar disturbance $d$ that is outside our control, which requires a modification of (2.6a):
$x(k+1) = F(x(k), u(k), d(k))$

The ultimate goal is to achieve these three objectives simultaneously:

- (a) Tracking: With $\hat{y}(k) = y(k) - r(k)$, $\lim_{k\to\infty} |\hat{y}(k)| = e_\infty$, with $e_\infty = 0$, or very small.
- (b) Disturbance rejection: The error $e_\infty$ is not highly sensitive to the disturbance $d$.
- (c) Tuned transient response (you know what kind of acceleration "feels right") when driving a car.

A special case is when the reference and disturbance are assumed independent of time (e.g., driving at constant speed with a steady headway). In this special case, suppose in addition that the disturbance is known. We might choose $u(k) = \phi(x(k),r(0),d(0))$, where the policy $\phi$ is designed for: $e_\infty = 0$. Typically, $\phi$ is designed so that the state is also convergent: $x(k) \to x(\infty)$ as $k\to\infty$. The limiting values satisfy

$^3$ See [337] and its references.
