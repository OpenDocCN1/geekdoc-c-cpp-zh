
It is a great pleasure and honour for us to participate to this volume in honor of Professor Leon Chua, whose contributions to Nonlinear Science are so outstanding. We dedicate to him this piece on a domain of Nonlinear Science and bifurcation theory, namely the analysis of dynamical systems behaving with very different time scales. As we explain below, we believe it is one area where Nonlinear Science could help find new ways to improve our understanding of Nature and to forecast catastrophic events.

## 1. Introduction

Earthquakes, like volcanic eruptions as well as other physical phenomena and perhaps also some kinds of socio-economical “revolutions”, show an abrupt transition from one state to another. We develop a first approach to this question by introducing an abstract model. In this model, one assumes that an earthquake results locally from the evolution of a time-dependent potential which distorts as time evolves. The catastrophic motion of geophysical plates is imaged as the rocking of a ball in a double-well potential when the two minima exchanges their relative stability properties. From the point of view of dynamical systems this model shows a “dynamical saddle-node” bifurcation. At the bifurcation a pair of fixed points, one locally stable, the other locally unstable, merge and vanish as a control parameter changes. This transition is intrinsic (not the result of an excitation from outside) and dynamical in the sense that, as the parameter changes slowly, the system quickly jumps within a time much shorter than the typical time of evolution of the external parameter. In earthquakes, this typical time of evolution is on geological scales of plate tectonics (typically hundred years for major earthquakes), although the duration of earthquakes is within the second to minute range. This saddle-node model is covered in Sec. 2 below.

Afterwards we examine another class of models, taken from the solid mechanics and geophysics literature which aimed at describing the relative slide of two plates subject to solid friction at their interface, one of them being pulled by an external spring driven at constant velocity.

In this second model, looked at in Sec. 3, and for realistic parameters values, there are relaxation oscillations of the stick-slip kind with widely different time scales, as in the case of the first model. However the responses to an external noise source are completely different for the two models. The first one displays the classical slowing-down of the fluctuations near the transition, with a progressive increase of the correlation time starting noticeably before the transition itself. In the stick-slip model on the contrary, the response to the noise becomes more and more short-memory as the transition approaches. While they present different character, the response to noise changes long before the transition in both models and so could be used to detect catastrophes.

## 2. Dynamical Double-well Model: Saddle-node Bifurcation

In this section, we consider a saddle-node bifurcation in a “gradient flow”, that is a damped dynamical system such that a coordinate $x(t)$ is solution of the equation of motion of the type

$$\frac{dx}{dt}=-\frac{\partial V}{\partial x}. \tag{1}$$

In this equation $V(x)$ is a potential, and the dynamics tends to lower the value of $V(x)$. In the geophysical context, the scalar variable $x$ could be the displacement of one plate with respect to the one it slides over. In the following we ultimately consider the case of a time dependent double well potential $V(x,t)$, distorting with time, of the form

$$V_q(x,t)=-\frac{x^3}{3}-atx+\frac{x^4}{4}. \tag{2}$$

illustrated in Fig. 1(b), where the three curves display the evolution of the potential as time evolves (see caption). In Eq. (2) the constant parameter $a$ gives the distortion rate, small value of $a$ corresponding to a slow distortion of the potential. The solution of the dynamical model (1)–(2) illustrated in Fig. 3 displays a jump from negative to positive values occurring at a time value $t_c$ named the transition time.

![](img/039e7d3c23390584a66737067db8b75b_381_0.png)

Note that the present approach differs from the catastrophe theory of Thom and Arnold [1] which studies how steady equilibria of equations like (1) change when some constant parameter of the potential $V(\cdot)$ is modified. Below we consider a different kind of question, namely what happens to the solution of equation (1) when the potential becomes itself a slowly varying function of time, like the potential (2) with the time dependent parameter $at$. We show in particular that the pair of equilibrium points disappears by a saddle-node bifurcation at $t=0$. While the question of rocking of the solution between two stationary steady state has been already studied [2] with various applications in mind, this question of the slow sweeping across bifurcations (by “sweeping” we mean crossing of a transition point with a time dependent parameter in the equation(s) of motion) has not been so much developed to the best of our knowledge. We emphasize the occurrence of an intermediate time scale in the case of a slow sweeping that has not been noticed before, although we believe it to be crucial for a strategy of foretelling catastrophes in the real world.

### 2.1. *Cubic potential just before the transition*

Before studying this quartic potential model, let us first investigate what happens in a close vicinity of the transition, for small values of $x$, where the potential reduces to a cubic expansion with respect to $x$. Assume first that $V(\cdot)$ does not depend explicitly on time and takes the form

$$V(x)=-\left(\frac{1}{3}x^3+bx\right), \tag{3}$$

with $b$ real constant (for the moment). For $b$ negative $V(x)$ has two real extrema (i.e. the roots of $\frac{\partial V}{\partial x}=0$), one $-\sqrt{-b}$ is a stable equilibrium, the other, $\sqrt{-b}$, is an unstable equilibrium. For $b=0$ the two equilibria merge and disappear for $b$ positive. This is the saddle-node bifurcation. The shape of $V(x)$ near $x=0$ and for $b$ small is universal: for a given smooth $V(x)$ showing this saddle-node bifurcation, one can always rescale time and external parameter to find the “local” problem in this form.

The extension to a time dependent control parameter $b$ goes as follows. If $b$ is a smooth function of time, one can assume that $b(t)$ crosses the critical value, i.e. zero in the present case, at time zero in such a way that $b(t)=at+\cdots$ with a nonzero constant, and the dots being for higher terms in the Taylor expansion of $b(t)$. The time dependent cubic potential becomes

$$V_c(x,t)=-\left(\frac{1}{3}x^3+atx\right), \tag{4}$$

evolving with time as illustrated in Fig. 1(a). With the rescaling $x\mapsto xa^{-1/3}$ and $t\mapsto ta^{1/3}$, the dynamical equation (1) corresponding to the cubic potential writes

$$\dot{x}=-(t+x^2), \tag{5}$$

which is the “universal” parameterless dynamical equation for a saddle-node bifurcation.

![](img/039e7d3c23390584a66737067db8b75b_382_0.png)
![](img/039e7d3c23390584a66737067db8b75b_382_1.png)

Fig. 2. (a) Solutions of Eq. (12), with and without noise. $\varepsilon_n = 0$ (smooth curve) and $\varepsilon_n = 1$ (noisy curve). With small amplitude noise the two curves cannot be distinguished. (b) A single sample of short memory noise $f(t)$.

#### 2.1.1. Van der Pol oscillation relaxations

We point out that this generic equation describes for example the transition from slow to fast motion in the van der Pol oscillator, as shown by Dorodnitsyn [3] and recalled here briefly. The van der Pol dynamical system

$$\ddot{x} + \eta(x^2 - 1)\dot{x} + x = 0, \tag{6}$$

is a prototype for relaxation oscillations (RO) with slow drift and fast jumps in saddle folding systems, in the limit of large non linearities (large positive $\eta$ values). Using the Liénard transform $y = -\dot{x}/\eta - \int_0^x (x^2 - 1)$, then setting $t \mapsto t/\eta$, equation (6) writes

$$\begin{cases}
\dot{y} = x, \\
\dot{x} = -\eta^2 \left[ y + \left(\frac{x^3}{3} - x\right) \right].
\end{cases} \tag{7}$$

which shows that the dominant component of the velocity field is $\dot{x}$ in the limit $\eta$ large. As well known the trajectory in the plane $(x, y)$ follows in the slow phases the cubic $y = x - x^3/3$, but becomes unstable at $x = \pm 1$, where it jumps along a line at $y$ almost constant toward $x = \pm 2$ on the cubic. Close to the transition point $(x = -1, y = -2/3)$, the equations of motion for $\delta x = x + 1$ small compared to one and $\delta y = y + 2/3$ write

$$\begin{cases}
\delta \dot{y} = -1, \\
\delta \dot{x} = -\eta^2 (\delta y - \delta x^2).
\end{cases} \tag{8}$$

which have the obvious solution $\delta y = -t + t_0$, $t_0$ constant, taken as zero, and $\delta \dot{x} = \eta^2(t + \delta x^2)$. The constant $\eta$ can be eliminated by taking as new time scale $t \mapsto \eta^{4/3} t$ and new variable $x \mapsto \delta x \, \eta^{2/3}$, which gives exactly the equation (5) introduced above to describe the dynamics near a saddle node bifurcation with a drifting parameter.

#### 2.1.2. Solution of the “universal” model

We look for a solution of equation (5) transiting from the “stable” fixed point at “large” negative times to the rolling down one towards positive value of $x$ at positive times. This solution behaves like $x(t) \approx -\sqrt{-t}$ at large negative times. The equation (5) is of the Riccati type and can be integrated by introducing the function $y(t)$ such that $x(t) = -y'/y$ where $y' = dy/dt$ and $y(t)$ is a solution of Airy’s equation,

$$y'' + t y = 0. \tag{9}$$

The solution relevant with the given condition for $x(t)$ at $t \to -\infty$, is Airy’s function $\mathrm{Ai}(-t)$ which writes

$$Y(t) = \mathrm{Ai}(-t) = \int_0^{+\infty} \cos\left( u^3/3 - u t \right) du, \tag{10}$$

and leads to the blue curve $x(t)$ drawn on Fig. 2(a). The transition ends up when $t$ becomes equal to the first zero of Airy’s function $\mathrm{Ai}(-t)$, corresponding to a divergence of the original function $x(t)$. Let $t_c$ be this critical value of $t$, i.e. the smallest root of $Y(t) = 0$, a pure number, about $t_c \approx 2.338$, corresponding to a divergence of the solution $x(t)$ of the cubic potential model. Just before the transition, the behavior of $x(t)$ deduced from the Laurent
