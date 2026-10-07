
# Unsteady, Non-Linear, and Chaotic Systems

thus the solution (4.98c) of (4.92b) is the product of a periodic function (4.97) by an exponential of time (4.98a). In the second case of coincident eigenvalues (4.96a) $\equiv (4.99a)$ it follows for (4.99b:

$s_* = s_- = s_0 = \exp(b_0 t), \quad x_*(t) = \exp(b_0 t)\varphi_*(t), \quad (4.99a, b)$

satisfies (4.96b, c) $\equiv$ (4.100a, b:

$\varphi_*(t+\tau) = e^{(b_*-b_*)t}x_*(t) = e^{(b_*-b_*)t}x_*(t) = e^{-b_0t}x_*(t) = \varphi_*(t), \quad (4.100a)$

$e^{-b_0t} [x_*(t) + x_*(t)] = \varphi_*(t) + \varphi_*(t); \quad (4.100b)$

and the functions $\varphi_*$ are periodic. It has been shown that a linear second-order (4.92a) ordinary differential equation (4.91b) with periodic coefficients (4.91a) has problem (92) solutions that are the product of a periodic function by an exponential of time (4.98c) with distinct characteristic exponents (4.98b) that are the eigenvalues (4.98a) of (4.98a). If the eigenvalues coincide (4.99a), the single characteristic exponent (4.99a) = (4.101a) appears (4.98b) in the solutions (4.96b, c) = (4.101b, b:

$s_* = s_- = s_0 = \exp(b_0t), \quad x_*(t) = e^{b_0t}\varphi_*(t), \quad x_*(t) = e^{-b_0t}[\varphi_*(t) + \varphi_*(t)], \quad (4.101a-c)$

where $\varphi_*$ and $\tau$ are periodic functions with period $\tau$.

## 4.3.5 Stability, Instability, and Indifference Boundary

In the preceding solutions the periodic functions are bounded (4.102a), ensuring that the growth for long time is determined by the exponential factor:

$\varphi_*(t) = |\varphi_*(t+\tau)| \leq M; \quad |x_*(t)| \leq e^{|b_*|t}|\varphi_*(t)| \leq M e^{|b_*|t}. \quad (4.102a, b)$

The characteristic exponent may be complex (4.94a) = (4.94b) and only the real part affects the modulus of the exponential (4.103a):

$b = \alpha + i\beta: \quad |e^b| = |e^{\alpha}e^{i\beta}| = e^\alpha \exp[Re b]. \quad (4.103a, b)$

Thus a linear-order-(4.92a) differential equation (4.91b) with periodic coefficients (4.91a) has general integral (4.104b) [=4.105b] if the characteristic exponents are distinct (4.104a) = equal(4.105a):

$b_+ \neq b_-: \quad x(t) = C_+x_*(t) + C_-x_-(t) = C_+e^{b_+t}\varphi_*(t) + C_-e^{b_-t}\varphi_-(t), \quad (4.104a, b)$

$b_+ = b_- = b_0: \quad x(t) = C_+x_*(t) + C_-x_-(t) = e^{b_0t}[(C_+ + C_-)\varphi_*(t) + \varphi_-(t)], \quad (4.105a, b)$

## Non-Linear Differential Equations and Dynamical Systems

where $\varphi_{\pm}(t)$ are periodic functions (4.102a) with period $\tau$. The limit for large time:

$Re(b_*) \geq Re(b_-): \quad \lim_{t\to\infty} |x(t)| = \begin{array}{rcl} = & \text{if} Re(b_*) > 0: & \text{instability} \neq 0, \infty & \text{if} Re(b_-) = 0: & \text{indifferent,} \ = 0 & \text{if} Re(b_-) < 0: & \text{stability,} \end{array};$
(4.106a–d)

shows that the exponent with larger real part (4.106a) determines: (i) stability if it is negative (4.106d); (ii) *instability* if it is positive (4.106b); and (iii) *indifference* if the value is zero (4.106c). The results are considered next for the variable undamped linear oscillator (subsection 4.3.2) showing that (subsection 4.3.6) only the cases (i) and (iii) occur.

## 4.3.6 Stability of the Linear Variable Oscillator

The preceding results (4.104a, b; 4.105a, b) apply to the undamped linear variable oscillator, for which the two terms in the case of distinct values (4.107a) may be written (4.107c) using the eigenvalues (4.107b):

$b_* \neq b_-: \quad \exp(b_*t)\varphi_*(t) = s_*'\varphi_*(t)$

The general integral for is (4.108b) for distinct (4.108a) [equal (4.109a)] eigenvalues:

$s_* \neq s_-: \quad x(t) = C_*s'\varphi_*(t) + C_-s'\varphi_-(t) = C_{x_*}(t) + C_{x_-}(t), \quad (4.108a, b)$

$s_* = s_- = s_0: \quad x(t) = s_0'[(C_* + C_-)\varphi_*(t) + \varphi_-(t)] = C_{x_*}(t) + C_{x_-}(t). \quad (4.109a, b)$

Since $x_*$ satisfy the differential equation (4.86b) = 4.110a, b follows 4.110c:

$\ddot{x}_* + \omega^2x_* = 0: \quad 0 = x_*\dot{x}_- - \dot{x}_*x_- = \frac{d}{dt}(x_*\dot{x}_- - \dot{x}_*x_-), \quad (4.110a–c)$

implying that the Wronskian (1.4c) is constant (4.111a):

$E = x_*(t)\dot{x}_-(t) - \dot{x}_*(t)x_-(t) = x_*(t+\tau)\dot{x}_-(t+\tau) - \dot{x}_*(t+\tau)x_-(t+\tau) = s_*_-E;$

## Unsteady, Non-Linear, and Chaotic Systems

the Wronskian is unchanged (4.111b) replacing $t$ by $t+\tau$, and (4.95b, c) lead to (4.111c). It follows (4.111c) = (4.112a) the product of eigenvalues is unity:

$s_+_- = 1; \quad \{s_+, s-\} = \{s_+', s_-'\} \quad \text{or} \quad \{s_+, s-\} = \{s_-', s_+'\}; \quad (4.112a-c)$

also, since the differential equation (4.86b) has real coefficients, both $x_\pm$ and $x_\pm$ are solutions and thus pairs of eigenvalues $s_\pm$ coincide with $s_\pm$ leading to (4.112b). In the first case $s_+$ is real (4.113a) and $s_-$ is different if they are not unit (4.114b, c) so that (4.108b) diverges for large $t$ (4.113d) to instability:

$s_+ = s_+^*; \quad s_- < 1, \quad s_- = \frac{1}{s_-^*} > 1, \quad b_+ > b_-; \quad (4.113a-e)$

corresponding (4.107c) to (4.113e). In the second case, $s_\pm$ are complex conjugate (4.114a) and never have unit modulus (4.114b, c) so that (4.108b) is finite (4.114d) for large

$s_+ = s_+^*; \quad 1 = s_+s_- = s_+_-^* = |s_+|^2, \quad \lim_{t\to\infty} |s_-|^{t/\tau} = 1, \quad \text{Re}(b_+) = 0; \quad (4.114a-e)$

corresponding (4.107c) to the difference $\equiv$ (4.106c). In the second case the eigenvalues (4.114a) with unit modulus (4.114b) can be written in the form (4.114f) leading to the solution (4.108) = (4.114g) that is oscillatory and bounded:

$s_\pm = \exp(\pm i\psi); \quad x(t) = C\exp(i\psi/\tau) + C\exp(-i\psi/\tau); \quad (4.114f)$

If the eigenvalues coincides from (4.113a-c) that they are both unit $s_\pm = 1$ and (4.107c) implies $b_0 = 0$ hence difference (4.106c). It been shown that for the linear damped variable oscillator (4.86b) the displacements (4.108b) [(4.109b)] with problem (93) distinct (equal) eigenvalues implies that there are two possible cases: (i) instability (4.113a-e) if the eigenvalues or characteristic exponents are real and distinct; (ii) oscillation difference, that is for complex conjugate (4.114a-e) or coincident eigenvalues or characteristic exponents. The determination of the characteristic exponents is illustrated (subsection 4.3.8) in the process of obtaining the exact solutions (subsection 4.3.9) of the Mathieu equation (4.89) involving trigonometric series (subsection 4.3.7).

## 4.3.7 Expansion of Mathieu Functions in Trigonometric Series

The solution of the Mathieu equation (4.89) may be sought in the form of a trigonometric series:

$w(\theta) = \sum_{m=-\infty}^{\infty} A_m \cos(m\theta) + \sum_{m=-\infty}^{\infty} B_m \sin(m\theta), \quad (4.115)$

that is similar to a Fourier series (II.5.188b) = (4.115) is more general than the Fourier series (II.5.188b) since the coefficients may not satisfy the formula for the coefficients (II.5.189a, b; II.5.190a, b). Substituting the trigonometric series (4.115) in the Mathieu equation (4.89) leads to:

$0 = \sum_{m=-\infty}^{\infty} [(a-m^2) \cos(m\theta) - 2q \cos(m\theta) \cos(2\theta)] A_m + \sum_{m=-\infty}^{\infty} [(a-m^2) \sin(m\theta) - 2q \sin(m\theta) \cos(2\theta)] B_m. \quad (4.116)$

Using the identities (II.5.88a) = (4.117a) and (II.5.88c) = (4.117b):

$2 \cos(m\theta) \cos(2\theta) = \cos[(m+2)\theta] + \cos[(m-2)\theta], \quad (4.117a)$

$2 \sin(m\theta) \cos(2\theta) = \sin[(m+2)\theta] + \sin[(m-2)\theta], \quad (4.117b)$

leads to:

$0 = \sum_{m=-\infty}^{\infty} [(a-m^2) A_m - q(A_{m+2} + A_{m-2})] \cos(m\theta) + \sum_{m=-\infty}^{\infty} [(a-m^2) B_m - q(B_{m+2} + B_{m-2})] \sin(m\theta). \quad (4.118)$

In order for the trigonometric series to vanish, all terms in square brackets must vanish, leading to the recurrence formulas for the coefficients.

## 4.3.8 Even/Odd Mathieu Functions with Period $\pi/2$

The vanishing of the coefficients in (4.118) leads to four cases: (i) the coefficients $A_m$ ($B_m$) of the cosines (sines) leads to solutions that are even (odd) functions of the variable $\theta$; and (ii) the coefficients are related by jumps of two
