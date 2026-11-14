n = 1. We assume they are verified for n, we prove them for n + 1. Since \( G_n(x, z) \) is K-convex in x, continuous and \( \to +\infty \) as \( x \to +\infty \), we can define \( s_n(z), S_n(z) \) with

(12.4.16) \( G_n(S_n(z), z) = \inf_\eta G_n(\eta, z) \)

(12.4.17) \( s_n(z) = \begin{cases} 0, & \text{if } G_n(0, z) \le K + \inf_\eta G_n(\eta, z) \\ G_n(s_n(z), z) = K + \inf_\eta G_n(\eta, z), & \text{if } G_n(0, z) > K + \inf_\eta G_n(\eta, z) \end{cases} \)

As usual we take the smallest minimum to define \( S_n(z) \) in a unique way. Since \( G_n(\eta, z) \) is continuous, it is easy to check that \( S_n(z) \) is continuous. Also \( s_n(z) \) is continuous.

We can write

\( u_{n+1}(x, z) = (h - c)x + G_n(\max(x, s_n(z)), z), \)

which shows immediately that \( u_{n+1}(x, z) \) is K-convex and continuous. Furthermore \( u_{n+1}(x, z) \to +\infty \), as \( x \to +\infty \). We then have

\( G_{n+1}(x, z) = cx + pE[(x - z_2)^+ | z_1 = z] + \alpha(h - c)E[(x - z_2)^+ | z_1 = z] + \alpha E[G_n(\max(x - z_2, s_n(z_2)), z_2) | z_1 = z] \)

It is the sum of a convex function and a K-convex function, hence K-convex. It is continuous and \( \to +\infty \) as \( x \to +\infty \). So the recurrence is proven. If we write (formally)

\( u'_n(x, z) = h - c + \chi_n(x, z), \)

then one has the recurrence

\( \chi_{n+1}(x, z) = \begin{cases} 0 & \text{if } x < s_n(z) \\ = \mu(x, z) + \alpha E[\chi_n(x - z_2, z_2) | z_1 = z] \end{cases} \)

with

(12.4.18) \( \mu(x, z) = c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x|z). \)

The function \( \chi_{n+1}(x, z) \) is discontinuous in \( s_n(z) \). However one has the bound

\( -\frac{(p - c)}{1 - \alpha} \le \chi_{n+1}(x, z) \le \frac{c + \alpha(h - c)}{1 - \alpha} \quad \text{a.e.} \)

Therefore the limit \( u(x, z) \) is K-convex and satisfies

\( u'(x, z) = h - c + \chi(x, z), \)

with

\( -\frac{(p - c)}{1 - \alpha} \le \chi(x, z) \le \frac{c + \alpha(h - c)}{1 - \alpha} \quad \text{a.e.} \)

Hence \( u(x, z) \) is continuous in x and \( \to +\infty \) as \( x \to +\infty \). Therefore one defines uniquely \( s(z), S(z) \) and \( S(z) \) minimizes in x the function

\( G(x, z) = cx + pE[(x - z_2)^+ | z_1 = z] + \alpha E[u((x - z_2)^+, z_2) | z_1 = z] \)

From this formula and the Lipschitz continuity of u in x, using the assumption (12.4.3) one can see that \( G(x, z) \) is continuous in both arguments. Hence \( S(z) \) and \( s(z) \) are continuous. The proof has been completed. \(\square\)