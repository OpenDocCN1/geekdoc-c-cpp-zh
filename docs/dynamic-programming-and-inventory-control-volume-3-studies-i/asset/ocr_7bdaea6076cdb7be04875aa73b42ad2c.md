After transformation we obtain

$$
\begin{aligned}
&\exp -\lambda L \sum_{k=0}^{s-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1) \left( x - \frac{[x]}{2} - \frac{s}{2} \right) \\
&+ \exp -\lambda L \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) \left( x - \frac{[x]}{2} - \frac{k}{2} \right) \\
&+ \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=s+1}^{[x]-j} \sum_{k=j+1}^{\infty} (x - j - s) \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \\
&- \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=[x]-j+1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \\
&- \sum_{j=[x]+1}^{\infty} \sum_{m=s+1}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}.
\end{aligned}
$$

# ## 14.9.2. LOCAL MINIMUM. We first have the derivative $\psi'_s(x + 0)$.

For $s < x < 0$

(14.9.3) $\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!}.$

We next consider the case $s < 0 < x$. We have

(14.9.4) $\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=[x]+1}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{\exp -\lambda L}{\lambda} \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} (h([x] - j + 1) + ps).$

Finally for $0 < s < x$ we have

(14.9.5) $\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=0}^{s-1} \frac{(\lambda L)^j}{j!} ([x] - s + 1) + \sum_{j=s}^{[x]} \frac{(\lambda L)^j}{j!} ([x] - j + 1) - \exp -\lambda L \sum_{j=[x]+1}^{[x]+s} \sum_{l=j+1-s}^{\infty} \frac{(\lambda L)^l}{l!} \sum_{k=[x]+1}^{j} C_l^{j-k} \right].$

We can check for $s < 0 < x$ the formula

$\psi'_s(x + 1 + 0) - \psi'_s(x + 0) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{[x]+1-s} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=[x]+2}^{[x]+1-s} \frac{(\lambda L)^j}{j!} \right].$