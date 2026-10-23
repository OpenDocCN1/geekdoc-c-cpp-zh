
![](img/039e7d3c23390584a66737067db8b75b_115_0.png)

But as \(f(x)_0 = F(x_{-1}, x_0, x_1)\) (3) and comparing (2) and (3), we see that \(f(x)_0\) may be distinct from \(f(y)_0\) if \(y_{-1} \ne x_{-1}\). This however will depend on the rule \(F\) and the values of \(x_{-1}\). If, for example, \(F\) does not depend explicitly on \(x_{-1}\), comparing (2) and (3) shows that \(f(x)_0 = f(y)_0\). However, \(F\) may depend on \(x\) without implying a distinction between \(f(x)_0\) and \(f(y)_0\) for some particular values of \(x\). In the following example: \(F(x_{-1}, x_0, x_1) = x_{-1} x_0 x_1\) and for \(x_0 = x_1 = 0\), we see that \(f(y)_0 = f(x)_0\) whatever the value of \(y_{-1}\). But if \(x_0 = x_1 = 1\) then \(f(y)_0 \ne f(x)_0\) as soon as \(y_{-1} \ne x_{-1}\). In this case we say that for this rule and this \(x\) configuration, the \(y\)-perturbation of \(x\) at site \(-1\) is propagated to the right. But how far can it spread? If we look at \(f(y)_1\) and we use the same formulas (1)–(3) to compute \(f(y)_1\), we see that \(f(y)_1 = f(x)_1\) since \(y_0 = x_0\), \(y_1 = x_1\), \(y_2 = x_2\), and consequently we have also \(f(y)_i = f(x)_i\) for all \(i \ge 1\). That is to say, the \(y\)-perturbation propagates, in one iteration, to at most one site to the right.

Now take more and more iterations of \(y\). For that, we use the following expression of \(f^2(y)_i\):

\(f^2(y)_i = F(f(y)_{i-1}, f(y)_i, f(y)_{i+1}) = F(F(y_{i-2}, y_{i-1}, y_i), F(y_{i-1}, y_i, y_{i+1}), F(y_i, y_{i+1}, y_{i+2}))\) (4)

and we apply it for \(i = 0,1,2,\dots\) From the definition of \(y\), we see that

\(f^2(y)_0 = F(F(y_{-2}, y_{-1}, y_0), F(y_{-1}, y_0, y_1), F(y_0, y_1, y_2)) = F(F(y_{-2}, y_{-1}, x_0), F(y_{-1}, x_0, x_1), F(x_0, x_1, x_2)).\)

Comparing \(f^2(y)_0\) with \(f^2(x)_0\) given by

\(f^2(x)_0 = F(F(x_{-2}, x_{-1}, x_0), F(x_{-1}, x_0, x_1), F(x_0, x_1, x_2))\) (5)

we see here, and we saw in the case of \(f(y)_0\), that the \(y\) perturbation at the site \(-2\) or \(-1\) may propagate to the site 0 too. Now, with this second iteration,

\(f^2(y)_1\) may now be distinct from \(f^2(x)_1\), i.e. from (4) we obtain:

\(f^2(y)_1 = F(F(y_{-1}, x_0, x_1), F(x_0, x_1, x_2), F(x_1, x_2, x_3))\) (6)

which can be distinct from \(f^2(x)_1\) when \(y_{-1} \ne x_{-1}\). Moreover, as above, looking at \(f^2(y)_2\), \(f^2(y)_3\), etc., the \(y\)-perturbation is propagated, in two iterations, at the far right at most to the second site. It is possible that this perturbation propagates also to the left of 0, but we focus only on the propagation to the right of the (left) perturbations of \(x\).

Therefore, doing more iterations, the perturbation propagates to the right step by step. The closest site to 0 never reached by any left perturbation \(y\) of \(x\) in \(n\) iterations is denoted by \(\widetilde{\Lambda}_n^+(x)\). \(\widetilde{\Lambda}_n^-(x)\) is defined in the same way for right perturbations of \(x\) that propagate to the left of the site 0.

It so happens that in this definition the site 0 plays a privileged role while the rule is translation invariant regardless of the site position. In order to make the definition shift invariant a new exponent is defined as

\(\Lambda_n^\pm(x) = \sup_{j\in\mathbb{Z}} \widetilde{\Lambda}_n^\pm(\sigma^j x)\) (7)

The time average speed of propagation (by unit time) is then defined as:

\(\lambda^\pm(x) = \lim_{n\to\infty} \frac{1}{n} \Lambda_n^\pm(x)\) (8)

This average speed was termed by Wolfram and Shereshevsky the left (in the case “-”) and right (in the case “+”) Lyapunov exponents. It can be proved using the Kingman subadditive ergodic theorem that the above limit indeed exists in the sense of measure theory (i.e. almost everywhere). Later on, a slightly different concept of an average Lyapunov exponent was given in [19].

It is interesting to see the above definition in one example of CA defined by the rule:

\(F(x_{-1}, x_0, x_1) = x_{-1} + x_0 \pmod 2.\)

The following scheme represents a space-time lattice, where the entering arrows to a site \(i\) at a time \(t\) correspond to the above rule.

It is easy to see that a perturbation \(y_{-1} \ne x_{-1}\) will propagate after \(n\) iterations to site \(n-1\),

![](img/039e7d3c23390584a66737067db8b75b_116_0.png)

Scheme of the action of the automaton at site \(i\) along time.

that is \(f^n(y)_{n-1} \ne f^n(x)_{n-1}\). This implies that \(\widetilde{\Lambda}_n^+(x) = n\). It is not the same for the left Lyapunov exponent which is obviously here vanishing. It follows then that \(\Lambda_n^+(x) = n\) and so \(\lambda^+(x) = 1\). In contrast, \(\lambda^-(x) = 0\).

In this example, it is the one-to-one property of the map \(x_{-1} \mapsto F(x_{-1}, x_0)\) which generates the maximal propagation to the right. In general a rule \(F\) such that \(x_{-1} \mapsto F(x_{-1}, \overline{x_0}, \overline{x_1})\) is one-to-one for any value of \(\overline{x_0}, \overline{x_1}\) is called by Hedlund [12] a left permutative rule. Right permutative rules are defined symmetrically. L. Chua et al. [2] showed that there are 28 rules that are left or right permutative; among them only 4 are left and right permutative. Hedlund [12] showed that any permutative rule defines a surjective CA. L. Chua et al. [2] introduced a class of rules called strongly quasi-ergodic by using the isomorphism between \(\{0,1\}^{\mathbb{Z}}\) and the interval \([0,1]\), they associated to each cellular automaton a map of this interval into itself. Many properties of this map and its relation to permutativity and attractors of the CA-map have been given. Those properties have not yet been studied rigorously in the framework of an infinite lattice \(\mathbb{Z}\). A slightly different concept of Lyapunov exponent has been given by Tisseur in [19].

## 3. Instability, Invariant Measures and Entropy

We saw in the previous section how the Lyapunov exponents measure the instability of the initial conditions. A topological classification of the attractors of CA has been investigated by Kurka and others [1] on the infinite lattice \(\mathbb{Z}\). In the finite case, the topology of an attractor may be complex as shown by Chua et al. [1], especially as the length of the lattice \(L \longrightarrow \infty\). In this case, on account of instability of the initial conditions and complexity of attractors, only statistical knowledge may be reasonable for an understanding of the system.

Two statistical approaches to CA are possible. The first one corresponds to the description of long time behaviour of the CA-dynamics, when we start from a set of random initial conditions. Such a statistical description is reminiscent of the equilibrium micro-canonical ensemble in statistical mechanics. The second one corresponds to convergence to equilibrium under the CA-map of non-invariant measures. Concerning this problem, the only results to our knowledge in this respect are given by [4, 14] for some special CA-rule.

Concerning the first problem, there may be different stationary probability measures, invariant under the CA-map \(f\) and the shift \(\sigma\), corresponding to disjoint attractors eventually. As in statistical mechanics, one considers a class of observables, we may conveniently identify them with the continuous functions \(\Phi\) on \(X\). Given an initial configuration \(x\), a probability measure on the set \(X\) of all configurations is given by the equality of time averages to ensemble averages

\[
\forall\Phi\quad \lim_{n\to\infty} \frac{1}{n} \sum_{k=0}^{n-1} \Phi(f^k x) = \int_X \Phi(x)\,d\mu(x).
\]

If it exists, this measure \(\mu\) depends on the initial condition \(x\). We do not go here into a full discussion of the above ergodic property of the CA, which may be very complicated, and not yet totally understood. It is therefore more practical, in studying the statistical property of a given CA-map \(f\), to consider a family of shift invariant measures and to try to extract from them a subfamily of \(f\)-invariant measures.

A large class of shift invariant measures is known. One of the most remarkable is the uniform Bernoulli measure where the probability of any sequence

\(x_{i_1}=j_1, x_{i_2}=j_2, \dots, x_{i_n}=j_n\)

is equal to \((\tfrac12)^n\). Let us call it \(\nu\). Nevertheless, this measure is \(f\)-invariant only for surjective CA-maps [12]. In the non-surjective case, the invariant measures are related to the geometric structure of the attractors that may be less simple than the Bernoulli measures, as computed using time averages in [11].

An important statistical quantity that characterizes the complexity of all trajectories of a dynamical system is the entropy.

Let us first start with the concept of topological entropy, so called because it depends on the concept of neighbourhood and topology of the configuration space. For Wolfram cellular automata a formal distance between two configurations \(x=(x_i)\), \(y=(y_i)\), \(i\in\mathbb{Z}\), is given by

\(d(x,y)=\sum_{i=-\infty}^{+\infty}\frac{|x_i-y_i|}{2^{|i|}}.\)

That is, if \(m_0\) is the radius of the window around zero where \(x_i=y_i\), \(|i|\le m_0\), then all those \(y\) correspond to \(\frac1{2^{m_0}}\) neighbourhood of \(x\).

For a dynamical system on a smooth surface, entropy characterizes how nearby trajectories may become distant and distinguishable. It is even more simple to illustrate this concept in cellular automata dynamical systems.

In the space-time diagram of a CA, let \(R(m,t)\) be the rectangle

\(\{(i,\tau)\in\mathbb{Z}\times\mathbb{N}, -m\le i\le m, 0\le\tau\le t\}.\)

![](img/039e7d3c23390584a66737067db8b75b_117_0.png)

Two configurations \(x,y\) are said to be distinguished in \(R(m,t)\), if for some \((i,\tau)\in R(m,t)\)

\((x(\tau))_i\ne (y(\tau))_i\)

where \(x(\tau)=f^{\tau}(x)\).

Let \(N(m,t)\) be the number of all such patterns generated by the CA-rule. As most of the CAs are not invertible, in general, starting from any initial conditions, the CA-patterns will end on some attractors. The scaling law of \(N(m,t)\) as \(t\longrightarrow\infty\) and \(m\longrightarrow\infty\) defines the topological entropy by:

\(h(f)=\lim_{m\to\infty}\lim_{t\to\infty}\frac{\log N(m,t)}{t}.\)

That is

\(N(m,t)\sim K\cdot e^{h(f)t},\)

\(m\longrightarrow\infty\), \(t\longrightarrow\infty\), where \(K\) may depend on \(m\). For example, for the shift CA-rule

\(N(m,t)=2^{2m+t+2}\).

Note that, in this example, the limit \(m\longrightarrow\infty\) is not important since the number of possible states by site is equal to 2, so that \(h(f)=\log 2\). This is the maximal possible value of \(h(f)\) among all rules. The scaling law of the increase of the number of patterns generated by the CA is related to the propagation of perturbations. In fact, two configurations that are initially identical on \(\{-m,\dots,m\}\) sites, will become distinguished in the space-time rectangle \(R(m,t)\) under the action of the CA-map, which propagates the perturbations from the outside of this interval. This enhances the number \(N(m,t)\). The rigorous computation of entropy for CA is still unsolved, although there are examples of rules where this entropy is “undecidable” [13]. Nevertheless several computations were obtained in case studies especially for bipermutative CAs [6, 18].

Another point of view to the entropy is offered by the Shannon and Kolmogorov-Sinai (K-S) entropy defined in terms of \(f\)-invariant measures \(\mu\), \(h_\mu(f)\). For a given CA-map, as there may be several invariant measures, there are several (K-S)-entropies corresponding to a multitude of attractors. The topological entropy is an upper bound of those (K-S)-entropies. The K-S entropies corresponding to various ergodic measures provide complete information about the CA-map, that can be completed by a multifractal analysis.

For any \(\sigma\)-ergodic or \(f\)-ergodic measure \(\mu\), Shereshevsky [17] showed the following inequality

\(h_\mu(f)\le h_\mu(\sigma)\cdot(\lambda^+ + \lambda^-)\)

where \(h_\mu(\sigma)\) is the K-S entropy of \(\sigma\). This inequality becomes an equality for bipermutative CA-rules.
