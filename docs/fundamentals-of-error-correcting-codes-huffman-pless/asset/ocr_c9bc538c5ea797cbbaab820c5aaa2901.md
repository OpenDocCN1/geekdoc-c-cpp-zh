since \((0 : 0 : 0)\) is not a projective point, the only time that singular points on \(\mathcal{F}_m(\mathbb{F}_q)\) can exist are when \(\gcd(m, q) \neq 1\); in that case every point on the curve is singular. So if \(m\) and \(q\) are relatively prime, \(\mathcal{F}_m(\mathbb{F}_q)\) is nonsingular.

# Exercise 773 The Fermat curve \(\mathcal{F}_m(\mathbb{F}_q)\) is defined in Example 13.3.1. Consider the curve \(\mathcal{F}_3(\mathbb{F}_q)\) given by \(x^3 + y^3 + z^3 = 0\).

+   (a) Find three projective points \((x : y : z)\) of \(\mathbb{P}^2(\mathbb{F}_2)\) on \(\mathcal{F}_3(\mathbb{F}_2)\).
+   (b) Find the nine projective points \((x : y : z)\) of \(\mathbb{P}^2(\mathbb{F}_4)\) on \(\mathcal{F}_3(\mathbb{F}_4)\).
+   (c) Find the nine projective points \((x : y : z)\) of \(\mathbb{P}^2(\mathbb{F}_8)\) on \(\mathcal{F}_3(\mathbb{F}_8)\). The field \(\mathbb{F}_8\) can be found in Example 3.4.3.

# Example 13.3.2 Let \(q = r^2\) where \(r\) is a prime power. The Hermitian curve \(\mathcal{H}_r(\mathbb{F}_q)\) is the projective plane curve over \(\mathbb{F}_q\) defined by \(f(x, y, z) = x^{r+1} - y^r z - y z^r = 0\).

In Exercise 774, you will show that \(\mathcal{H}_r(\mathbb{F}_q)\) has only one point at infinity, namely \((0 : 1 : 0)\). We show that there are \(r^3\) affine points \((x : y : 1)\) of \(\mathbb{P}^2(\mathbb{F}_q)\) on \(\mathcal{H}_r(\mathbb{F}_q)\). As \(z = 1\), \(x^{r+1} = y^r + y\). But \(y^r + y = \text{Tr}_2(y)\), where \(\text{Tr}_2 : \mathbb{F}_{r^2} \to \mathbb{F}_r\) is the trace map from \(\mathbb{F}_{r^2}\) to \(\mathbb{F}_r\). As its image is a nonzero subspace of the 1-dimensional space \(\mathbb{F}_r\), \(\text{Tr}_2\) is surjective. So its kernel is a 1-dimensional subspace of \(\mathbb{F}_{r^2}\), implying there are \(r\) elements \(y \in \mathbb{F}_{r^2}\) with \(\text{Tr}_2(y) = 0\). When \(\text{Tr}_2(y) = 0\), then \(x^{r+1} = 0\) has one solution \(x = 0\); this leads to \(r\) affine points on \(\mathcal{H}_r(\mathbb{F}_q)\). If \(x \in \mathbb{F}_{r^2}\), \(x^{r+1} = x^r x = (r + 1)(x - 1) = 0\) and the nonzero elements of \(\mathbb{F}_{r^2}\) in \(x_{r+1}\) are precisely those satisfying \(\beta^{r-1} = 1\). When \(y\) is one of the \(r^2 - r\) elements of \(\mathbb{F}_{r^2}\) with \(\text{Tr}_2(y) \neq 0\), there are \(r + 1\) solutions \(x \in \mathbb{F}_{r^2}\) with \(x^{r+1} = \text{Tr}_2(y)\). This leads to \((r^2 - r)(r + 1) = r^3 - r\) more affine points. Hence, \(\mathcal{H}_r(\mathbb{F}_q)\) has \(r^3 - r + r = r^3\) affine points and a total of \(r^3 + 1\) projective points.

# Exercise 774 Let \(q = r^2\) where \(r\) is a prime power. The Hermitian curve \(\mathcal{H}_r(\mathbb{F}_q)\) is defined in Example 13.3.2.

+   (a) Show that \(\mathcal{H}_r(\mathbb{F}_q)\) is nonsingular. Hint: In \(\mathbb{F}_q\), \(r = 0\) as \(r\) is a multiple of the characteristic of \(\mathbb{F}_q\).
+   (b) Show that \((0 : 1 : 0)\) is the only point at infinity on \(\mathcal{H}_r(\mathbb{F}_q)\).
+   (c) Find the eight affine points \((x : y : 0)\) of \(\mathbb{P}^2(\mathbb{F}_4)\) on \(\mathcal{H}_2(\mathbb{F}_4)\).
+   (d) Find the 64 affine points \((x : y : 1)\) of \(\mathbb{P}^2(\mathbb{F}_{16})\) on \(\mathcal{H}_4(\mathbb{F}_{16})\). Table 5.1 gives the field \(\mathbb{F}_{16}\).

# Exercise 775 The Klein quartic \(\mathcal{K}_4(\mathbb{F}_q)\) is the projective curve over \(\mathbb{F}_q\) defined by the fourth degree homogeneous polynomial equation \(f(x, y, z) = x^3 y + y^3 z + z^3 x = 0\).

+   (a) Find the three partial derivatives of \(f\).
+   (b) Show that if \(\mathbb{F}_q\) has characteristic 3, \(\mathcal{K}_4(\mathbb{F}_q)\) is nonsingular.
+   (c) If \((x : y : z)\) is a singular point of \(\mathcal{K}_4(\mathbb{F}_q)\), show that \(x^3 = -3y^3 z\) using \(f(x, y, z) = 0\), and that \(z^3 x = 9y^3 z\) using \(f_x(x, y, z) = 0\) and \(f_z(x, y, z) = 0\).
+   (d) If \((x : y : z)\) is a singular point of \(\mathcal{K}_4(\mathbb{F}_q)\), show that \(7y^3 z = 0\) using \(x^3 y + y^3 z + z^3 x = 0\) and part (c).
+   (e) Using part (d), show that if \(\mathbb{F}_q\) does not have characteristic 7, then \(\mathcal{K}_4(\mathbb{F}_q)\) is nonsingular.
+   (f) Find the three projective points in \(\mathbb{P}^2(\mathbb{F}_2)\) on \(\mathcal{K}_4(\mathbb{F}_2)\).
+   (g) Find the five projective points in \(\mathbb{P}^2(\mathbb{F}_4)\) on \(\mathcal{K}_4(\mathbb{F}_4)\).