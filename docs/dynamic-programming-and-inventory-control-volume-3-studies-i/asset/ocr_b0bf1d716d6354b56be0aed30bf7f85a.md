where the random variables \( D^j \) are independent and have Poisson distributions (with parameters \( \lambda^j \)), then define

\(\gamma^j(x) = E\psi \left( x - \sum_{i=1}^j D_i \right), \gamma^0(x) = \psi(x).\)

Clearly \(\chi(x) = \gamma^j(x)\).

# **Exercise 11.9.** Prove that

\(\gamma^j(x) = E\gamma^{j-1}(x - D_j).\)

Since each of the demands has a Poisson distribution, one can checks recursively, that there exists a \( b \) such that \(\chi(x)\) is decreasing on \((-\infty, b]\), and \( K \) nondecreasing on \([b, +\infty)\).

We are in a position to solve the multi supplier problem. It is convenient to introduce the operator, for which \( w \) in equation (11.2.6) is a fixed point. More precisely, introduce functions \( v(x) \) such that

+   (11.2.12) 
+   \( v \) is continuous, \( (c_M + \alpha h)x + \alpha v(x) \to +\infty \), as \( x \to +\infty \) 
+   \( (c_1 - \alpha p)x + \alpha v(x) \to +\infty \), as \( x \to -\infty \) 
+   \( v(x) + c_M x \) is decreasing on \((-\infty, 0]\) 
+   \( v(x) + c_i x \) is \( K_i \) nondecreasing on \( R \)

Note that, from the third condition, we have also

\( v(x) \to +\infty, \text{ as } x \to -\infty. \)

We introduce the operator which associates to the function \( v(x) \), successively the functions

\( g_i(v)(x) = c_i(x + \overline{D}) + \alpha(hx^+ + px^-) + \alpha v(x), \)

and

\( G_i(v)(x) = Eg_i(v)(x - D). \)

Let also

\( G_i^*(v)(x) = \inf_{y \ge x} (K_i \mathbf{1}_{y > x} + G_i(v)(y)), \)

and

\( w_i(v)(x) = -c_i x + G_i^*(v)(x), \) 
\( w(v)(x) = \min_{1 \le i \le M} w_i(v)(x). \)

Then, we can assert that

\( w(x) = w(w)(x). \)

We begin with the

# **Lemma 11.3.** Assume (11.2.7) and that the demand \( D \) satisfies the property \( \mathcal{P} \). Skipping \( v \) in the notation of \( G_i(v) \), we can state that

+   (11.2.13) 
+   \( G_i \text{ is continuous, } G_i \to +\infty, \text{ as } |x| \to +\infty \) 
+   \( \exists a_i \ge 0 \text{ such that } G_i \text{ is decreasing on } (-\infty, a_i]. \) 
+   \( G_i \text{ is non } K_i \text{ decreasing on } (a_i, +\infty) \)