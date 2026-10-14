
of the Sobolev embedding was the question of prescribing the Gaussian curvature. Our approach is from this point of view. To explain the context let us recall some notions from geometry.

Let $(M, g)$ be a Riemannian manifold of dimension $n$ and $P_{1,g}$ be the conformal Laplacian defined by

$P_{1,g} = -\Delta_g + \frac{n-2}{4(n-1)} R_g,$

where $R_g$ is the scalar curvature of the metric. We know that if $\tilde g = e^{2u} g$ is a metric conformal to $g$, then

$P_{1,\tilde g}(v) = e^{-\left(\frac{n+2}{2}\right)u} P_{1,g}\left(e^{\left(\frac{n-2}{2}\right)u} v\right),$

for all smooth functions $v$. Paneitz introduces a fourth order operator $P_{2,g}$ of the form

$P_{2,g} = \Delta_g^2 + \text{lower order terms}$

and Branson found a sixth order operator $P_{3,g}$ of the form

$P_{3,g} = \Delta_g^3 + \text{lower order terms}$

with the conformal invariance properties. The existence of a general conformal operator of higher-degree was obtained by Graham, Jenne, Mason, and Sparling (what is popularly known as GJMS operators). They proved

## Theorem 9.8
Let $(M, g)$ be a Riemannian manifold of even dimension $n$. For $k \in \left\{1,2,\dots,\frac{n}{2}\right\}$ there exists a conformally invariant differential operator $P_{k,g}$ of the form

$P_{k,g} = \Delta_g^k + \text{lower order terms}$

satisfying,

$P_{k,\tilde g}(v) = e^{-\left(\frac{n+2k}{2}\right)u} P_{k,g}\left(e^{\left(\frac{n-2k}{2}\right)u} v\right)$

for a conformal metric $\tilde g = e^{2u} g$.

When $n$ is even and $k > \frac{n}{2}$, a conformally invariant operator $P_{k,g}$ with the above properties may not exist in general. For this reason $P_{\frac{n}{2},g}$ is known as the critical GJMS operator.

Observe that one can recover the scalar curvature of a metric by acting $P_{1,g}$ on the constant function. Similarly we define higher order curvatures known as $Q_k$ curvature for a Riemannian manifold $(M, g)$ of even dimension $n$. Let $k$ be an integer satisfying $k < \frac{n}{2}$ then the $Q_k$ curvature is defined by

$Q_k = \frac{2(-1)^k}{n-2k} P_k(1)$

and $Q_{\frac{n}{2}}$ curvature is defined using analytic continuation in the above formulae.

Similar to Gaussian curvature, the change of $Q_{\frac{n}{2}}$ curvature under a conformal change of the metric is governed by the GJMS operator. Let $\tilde{g}=e^{2u}g$ be a conformal metric on $(M,g)$, then $Q_{\frac{n}{2},g}$ and $Q_{\frac{n}{2},\tilde{g}}$ are related by the relation

$$P_{\frac{n}{2},g}(u)+Q_{\frac{n}{2},g}=Q_{\frac{n}{2},\tilde{g}}\,e^{nu}\tag{9.18}$$

One can easily see that solutions of the above equations are the critical points of the energy $J$ given by

$$J(u)=\frac{1}{2}\int_{M}P_{k}(u)u\,dV_{g}+\int_{M}Q_{k,g}u\,dV_{g}-\frac{1}{N}\int_{M}Q_{k,\tilde{g}}e^{nu}\,dV_{g}\tag{9.19}$$

where $k=\frac{n}{2}$.

A natural space where one would like to pose this functional is the space where $\int_{M}P_{k}(u)u\,dV_{g}<\infty$. Then one would like to know whether we can control $\int_{M}e^{nu}\,dV_{g}$ in terms of $\int_{M}P_{k}(u)u\,dV_{g}$. We answered these questions positively in [24]. We will briefly discuss the main results.

First let us recall the definition of the Sobolev space $H^{k}(\mathbb{H}^{n})$. We define the space $H^{k}(\mathbb{H}^{n})$ as the completion of $C_{c}^{\infty}(\mathbb{H}^{n})$ with respect to the norm

$$||u||_{H^{k}(\mathbb{H}^{n})}:=[\sum_{m=0}^{k}\int_{\mathbb{H}^{n}}|\nabla_{g}^{m}u|_{g}^{2}\,dv_{g}]^{\frac{1}{2}},$$

It is well known that we have the Poincaré inequality

$$\left(\frac{n-1}{2}\right)^{2}\int_{\mathbb{H}^{n}}u_{g}^{2}\,dv_{g}\le\int_{\mathbb{H}^{n}}|\nabla_{g}u|_{g}^{2}\,dv_{g}$$

holds for all $u\in H^{1}(\mathbb{H}^{n})$. We also have

$$\int_{\mathbb{H}^{n}}|\nabla_{g}u|_{g}^{2}\,dv_{g}=\int_{\mathbb{H}^{n}}- (\Delta_{g}u)u\,dv_{g}\le\left(\int_{\mathbb{H}^{n}}|\Delta_{g}u|^{2}\,dv_{g}\right)^{\frac{1}{2}}\left(\int_{\mathbb{H}^{n}}u^{2}\,dv_{g}\right)^{\frac{1}{2}}$$

Combining the above two inequalities and an induction argument gives us the following higher order Poincaré type inequality:

Let $k,l$ be non-negative integers such that $l<k$, then

$$\left(\frac{N-1}{2}\right)^{2(k-l)}\int_{\mathbb{H}^{n}}|\nabla_{g}^{l}u|_{g}^{2}\,dv_{g}\le\int_{\mathbb{H}^{n}}|\nabla_{g}^{k}u|_{g}^{2}\,dv_{g}$$

holds for all $u\in H^{k}(\mathbb{H}^{n})$.

As a consequence we see that the norm $\|u\|_{H^k(\mathbb{H}^n)}$ defined by

$$\|u\|_{H^k(\mathbb{H}^n)}:=\left[\int_{\mathbb{H}^n}|\nabla_g^k u|^2\,dv_g\right]^{\frac12},\qquad u\in H^k(\mathbb{H}^n)$$

defines an equivalent norm in $H^k(\mathbb{H}^n)$.

Next we define $\|\cdot\|_{k,g}$ by

$$\|u\|_{k,g}:=\left[\int_{\mathbb{H}^n}(P_k u)u\,dv_g\right]^{\frac12},\qquad u\in C_0^\infty(\mathbb{H}^n),$$

then we have:

## Lemma 9.2
*(Karmakar, Sandeep [24])*

Let $\|\cdot\|_{k,g}$ be as above then it defines a norm on $C_0^\infty(\mathbb{H}^n)$ for $2k\le n$. Moreover when $n=2k$ there exists a positive constant $\Theta$ such that

$$\frac{1}{\Theta}\|u\|_{k,g}\le \|u\|_{H^k(\mathbb{H}^n)}\le \Theta\|u\|_{k,g},$$

for all $u\in C_0^\infty(\mathbb{H}^n)$.

Using this norm $\|\cdot\|_{k,g}$ we established an Adams type inequality in $\mathbb{H}^n$.

## Theorem 9.9
*(Karmakar, Sandeep [24])*

Let $\mathbb{H}^n$ be the $n$ dimensional hyperbolic space with $n$ even and $k=\frac n2$ then,

$$\sup_{u\in C_0^\infty(\mathbb{H}^n),\ \|u\|_{k,g}\le1}\int_{\mathbb{H}^n}(e^{\beta u^2}-1)\,dv_g<+\infty$$

iff $\beta\le\beta_0(k,n)$, where $\beta_0(k,n)$ is as before.

Recall that a version of Adams inequality on $\mathbb{H}^n$ was obtained by Fontana and Morpurgo in [23]. A natural question is how does Theorem 9.8 compare with the inequality in [23]. For $n=4,\ 6,\ 8$ we can check that $\|u\|_{k,g}<\int_{\mathbb{H}^n}|\nabla^k u|^2$. Thus our inequality implies the one obtained by Fontana and Morpurgo.

To complete our aim we investigated the existence of PDEs of the form in Equation (9.18) using the Adams inequality in Equation (9.18). We could show that negative $Q_{k,\hat g}$ curvature which are $L^2$ perturbations of $Q_{k,g}$ can be prescribed. More generally we proved

## Theorem 9.10
*(Karmakar, Sandeep [24])*

Suppose $Q_1-Q_2\in L^2(\mathbb{H}^n)$ and $Q_2\le0$ then the equation

$$P_k(u)+Q_1=Q_2e^{nu}$$

has a solution in $H^k(\mathbb{H}^n)$.

Study of Moser–Trudinger and Adams inequalities continues to be an active area of research and many interesting results have come out after the above-described results were established, for example, some other versions were established in [25], Adams was established in the case of pinched Hadamard manifold in [26], etc.

## References

- 1. Pohozhaev, S.I. The Sobolev imbedding in the case p l = n, In: Proc. Tech. Sci. Conf. on Adv. Sci. Research 1964–1965, Mathematics Section, pp. 158–170. Moskov. Energet. Inst., Moscow, 1965.
- 2. Trudinger, Neil S. On imbeddings into Orlicz spaces and some applications, J. Math. Mech. 17, 473–483, 1967.
- 3. Moser, J. A sharp form of an inequality by N. Trudinger, Indiana Univ. Math. J. 20, 1077–1092, 1970/71.
- 4. Carleson, Lennart, and Chang, Sun-Yung A. On the existence of an extremal function for an inequality of J. Moser, Bull. Sci. Math. 110(2), 113–127, 1986.
- 5. Flucher, M. Extremal functions for the Trudinger-Moser inequality in 2 dimensions, Comment. Math. Helv. 67, 471–497, 1992.
- 6. Adimurthi , and Druet, O.. Blow-up analysis in dimension 2 and a sharp form of Trudinger-Moser inequality, Comm. Partial Diff. Equat. 29(1–2), 295–322, 2004.
- 7. Cao, D. Nontrivial solution of semilinear elliptic equations with critical exponent in R², Commun. Partial Diff. Equat. 17, 407–435, 1992.
- 8. Panda, R. Nontrivial solution of a quasilinear elliptic equation with critical growth in Rⁿ, Proc. Indian Acad. Sci. 105, 425–444, 1995.
- 9. do Ó, J.M. N-Laplacian equations in Rᴺ with critical growth, Abstr. Appl. Anal. 2, 301–315, 1997.
- 10. Ruf, B. A sharp Trudinger-Moser type inequality for unbounded domains in R², J. Funct. Anal. 219(2), 340–367, 2005.
- 11. Li, Y., and Ruf, B. A sharp Trudinger-Moser type inequality for unbounded domains in Rᴺ, Indiana Univ. Math. J. 57(1), 451–480, 2008.
- 12. Onofri, E. On the positivity of the effective action in a theory of random surfaces, Comm. Math. Phys. 86(3), 321–326, 1982.
- 13. Beckner, William. Sharp Sobolev inequalities on the sphere and the Moser-Trudinger inequality, Ann. of Math. 138(1), 213–242, 1993.
- 14. Cherrier, Pascal. Une inégalité de Sobolev sur les variétés riemanniennes, Bull. Sci. Math. 103(4), 353–374, 1979.
- 15. Fontana, Luigi. Sharp borderline Sobolev inequalities on compact Riemannian manifolds, Comment. Math. Helv. 68(3), 415–454, 1993.
- 16. Mancini, G., and Sandeep, K. Moser-Trudinger inequality on conformal discs, Commun. Contemp. Math. 12(6), 1055–1068, 2010.
- 17. Battaglia, Luca, and Mancini, Gabriele. Remarks on the Moser-Trudinger inequality, Adv. Nonlinear Anal. 2(4), 389–425, 2013.
- 18. Lu, G., and Tang, H. Best constants for Moser-Trudinger inequalities on high dimensional hyperbolic spaces, Adv. Nonlinear Stud. 13(4), 1035–1052, 2013.
- 19. Mancini, G., Sandeep, K., and Tintarev, C. Trudinger-Moser inequality in the hyperbolic space Hⁿ, Adv. Nonlinear Anal. 2(3), 309–324, 2013.
- 20. Adimurthi , and Tinterev, K. On a version of Trudinger-Moser inequality with Möbius shift invariance, Calc. Var. Part. Diff. Equat. 39(1–2), 203–212, 2010.
- 21. Yang, Qiaohua, Su, Dan, and Kong, Yinying. Sharp Moser-Trudinger inequalities on Riemannian manifolds with negative curvature. Ann. Mat. Pura Appl. 195(2), 459–471, 2016.
- 22. Adams, D.R. A sharp inequality of J. Moser for higher order derivatives, Ann. Math. 128, 385–398, 1988.
