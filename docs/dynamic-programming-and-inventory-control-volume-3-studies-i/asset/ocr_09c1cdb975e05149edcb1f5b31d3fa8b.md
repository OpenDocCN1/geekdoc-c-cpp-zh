From the above expression, using $c_m \le c_i, \forall i$, and the fact that $a_m \ge 0$, hence $G_m(x)$ is decreasing on $(-\infty, 0]$, the second part of Corollary 11.2 follows.

# 11.2.3. APPLICATION TO THE MULTI-SUPPLIER PROBLEM.

To apply the preceding results to the multi-supplier problem, we need an additional intermediary result. Consider a function $\psi(x)$, piece wise continuous, which tends to $+\infty$ as $|x| 	o +\infty$, hence attains its minimum. Let $D$ be a positive random variable, with density $f$. The quantity $\chi(x) = E\psi(x - D)$, is a continuous function, which also tends to $+\infty$ as $x 	o +\infty$.

Exercise 11.6. Prove the preceding property. Use the fact that $\psi(x)$ reaches its minimum.

However, if $\psi$ decreases on $(-\infty, a]$, and is non $K$ decreasing, on $[a, +\infty)$, then this property does not carry over to $\chi$. The same bad situation occurs whenever $\psi$ is quasi $K$ convex. In the case of $K$ convexity, the property carries over. Note however, that $\chi(x)$ decreases on $(-\infty, a]$, and since it goes to $+\infty$ as $x 	o +\infty$, there is necessarily some $b \ge a$, such that $\chi(x)$ decreases on $(-\infty, b]$, and may increase after. So $b$ is a local minimum. We want to restrict ourselves to distributions $f$ such that the following property $\mathcal{P}$ holds: The function $\chi$ is non $K$ decreasing on $[b, +\infty)$. 

Let us show that the property $\mathcal{P}$ holds, whenever the distribution $f$ is Poisson, or a convolution of Poisson distributions. Suppose $f$ is a Poisson distribution, with parameter $\lambda$, then $f(x) = \lambda \exp -\lambda x$.

Exercise 11.7. Check that $\chi'(x) = \lambda(\psi(x) - \chi(x))$.

Let $S$ be the minimum of $\chi$. Since $\chi'(b) = \chi'(S) = 0$, we have $\chi(S) = \psi(S)$ and $\chi(b) = \psi(b)$. Let $h > 0$. Consider the function $z(x) = \chi(x) - \chi(x + h) - K$, then we have $z(b) \le \chi(b) - \chi(S) - K = \psi(b) - \psi(S) - K \le 0$, since $a \le b \le S$.

Exercise 11.8. Check that $z'(x) \le -\lambda z(x)$. 

Therefore $\frac{dz}{dx} \exp \lambda x \le 0$, 

and it follows that $z(x) \exp \lambda x \le z(b) \exp \lambda b, \forall x \ge b$, hence $z(x) \le 0, \forall x \ge b$. This implies that $\chi$ is $K$ nondecreasing for $x \ge b$. The property $\mathcal{P}$ carries over to convolutions of Poisson distributions. Indeed, if $D = \sum_{j=1}^J D_j$,