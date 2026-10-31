**Proof:**

Since $C = Ef(S/E)$, from (RE-3.5),

$$\begin{aligned}
\frac{\partial C}{\partial E} &= \frac{\partial}{\partial E}[Ef(S/E)] \\
&= f(S/E) + E\frac{\partial f(S/E)}{\partial E} \\
&= f(S/E)\cdot 1 + E\cdot S\left(-\frac{1}{E^2}\right)\frac{\partial f}{\partial E} \\
&= f(S/E) - (S/E)f'(S/E)
\end{aligned}$$

therefore, upon substituting for $f(S/E)$ from (RE-3.6):

$$\frac{\partial C}{\partial E} = C/E - (S/E)F'(S/E) \tag{RE-3.8}$$

Again, since $C = Ef(S/E)$, from (RE-3.4),

$$\begin{aligned}
\frac{\partial C}{\partial S} &= \frac{\partial}{\partial S}[C] \\
&= \frac{\partial}{\partial S}[Ef(S/E)] \\
&= E\frac{\partial}{\partial S}[f(S/E)] \\
&= E(1/E)\frac{\partial}{\partial S}[f(S/E)] \\
&= (1)f'(S/E) \\
&= f'(S/E)
\end{aligned}$$

Therefore,

$$\frac{\partial C}{\partial S} = f'(S/E) \tag{RE-3.9}$$

or

$$\frac{\partial C}{\partial S} = f'(S/E) = f'$$

Hence,

$$S\frac{\partial C}{\partial S} = Sf'(S/E) = Sf'$$

Again, from (RE-3.5),

$$C = Ef(S/E)$$

Therefore,

$$\begin{aligned}
\frac{\partial C}{\partial S} &= \frac{\partial}{\partial S}[Ef(S/E)] \\
&= (1/E)\frac{\partial}{\partial S}[Ef(S/E)] \\
&= \frac{\partial}{\partial S}(Ef(S/E)] \\
&= f'(S/E)
\end{aligned} \tag{RE-3.10}$$