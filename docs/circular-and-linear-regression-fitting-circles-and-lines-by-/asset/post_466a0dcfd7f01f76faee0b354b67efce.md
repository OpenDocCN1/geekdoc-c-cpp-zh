
for the Taubin fit, see (5.48); here we again use our standard “sample mean” notation $\bar{z} = \frac{1}{n} \sum z_i$, etc.

**Reduction to a generalized eigenvalue problem.** To solve the constrained minimization problem (5.62)–(5.63) one uses a Lagrange multiplier $\boldsymbol{\eta}$ and reduces it to an unconstrained minimization of the function

$$\mathscr{G}(\mathbf{A}, \boldsymbol{\eta}) = \mathbf{A}^T \mathbf{M} \mathbf{A} - \boldsymbol{\eta}(\boldsymbol{\eta}^T \mathbf{N} \mathbf{A} - 1).$$

Differentiating with respect to $\mathbf{A}$ and $\boldsymbol{\eta}$ gives

$$\mathbf{M}\mathbf{A} = \boldsymbol{\eta}\mathbf{N}\mathbf{A} \qquad \qquad \qquad (5.68)$$

and

$$\mathbf{A}^T \mathbf{N} \mathbf{A} = 1, \qquad \qquad \qquad \qquad (5.69)$$

thus $\mathbf{A}$ must be a generalized eigenvector for the matrix pair $(\mathbf{M}, \mathbf{N})$, which also satisfies $\mathbf{A}^T \mathbf{N} \mathbf{A} = 1$. The problem (5.68)–(5.69) may have several solutions. To choose the right one we note that for each solution $(\boldsymbol{\eta}, \mathbf{A})$ we have

$$\mathbf{A}^T \mathbf{M} \mathbf{A} = \boldsymbol{\eta}\mathbf{A}^T \mathbf{N} \mathbf{A} = \boldsymbol{\eta}, \qquad \qquad (5.70)$$

thus for the purpose of minimizing $\mathbf{A}^T \mathbf{M} \mathbf{A}$ we should choose the solution of (5.68)–(5.69) with the smallest $\boldsymbol{\eta}$. Note that $\boldsymbol{\eta}$ is automatically nonnegative, since $\mathbf{M} = \frac{1}{n}\mathbf{X}^T\mathbf{X}$ is a positive semi-definite matrix.

Since multiplying $\mathbf{A}$ by a scalar does not change the circle it represents, it is common in practical applications to require that $\|\mathbf{A}\|=1$, instead of $\mathbf{A}^T \mathbf{N} \mathbf{A}=1$. Accordingly one needs to replace the rigid constraint (5.69) with a softer one $\mathbf{A}^T \mathbf{N} \mathbf{A}>0$. The latter can be further relaxed as follows.

For generic data sets, $\mathbf{M}$ is positive definite. Thus if $(\boldsymbol{\eta},\mathbf{A})$ is any solution of the generalized eigenvalue problem (5.68), then $\mathbf{A}^T \mathbf{M} \mathbf{A} > 0$. In that case, due to (5.70), we have $\mathbf{A}^T \mathbf{N} \mathbf{A} > 0$ if and only if $\boldsymbol{\eta} > 0$. Thus it is enough to solve the problem (5.68) and choose the smallest positive $\boldsymbol{\eta}$ and the corresponding unit vector $\mathbf{A}$. This rule is almost universally used in practice. However, it needs to be adapted to one special case, which turns out to be quite precarious.

**The singular case.** The matrix $\mathbf{M}$ is singular if and only if the observed points lie on a circle (or a line); in this case the eigenvector $\mathbf{A}_0$ corresponding to $\boldsymbol{\eta} = 0$ satisfies $\mathbf{X}\mathbf{A}_0 = \mathbf{0}$, i.e., it gives the interpolating circle (line), which is obviously the best possible fit. However, it may happen that for some (poorly chosen) matrices $\mathbf{N}$ we have $\mathbf{A}_0^T\mathbf{N}\mathbf{A}_0 < 0$, so that the geometrically perfect solution fails to satisfy the “soft” constraint $\mathbf{A}^T\mathbf{N}\mathbf{A} > 0$, and thus has to be rejected. Such algebraic fits are poorly designed and not worth considering.

For all the constraint matrices $\mathbf{N}$ mentioned so far we have $\mathbf{A}^T \mathbf{N} \mathbf{A} \ge 0$ whenever $\mathbf{A}^T \mathbf{M} \mathbf{A} = 0$. For example, the Kåsa matrix $\mathbf{K}$, the Taubin matrix $\mathbf{T}$, and the constraint matrices corresponding to the Gander-Golub-Strebel fit and the Nivergelt fit (Section 5.8), are all positive semi-definite, hence $\mathbf{A}^T \mathbf{NA} \geq 0$ for any vector $\mathbf{A}$. The Pratt matrix $\mathbf{P}$ is not positive semi-definite, but we have seen that $\mathbf{A}^T \mathbf{PA} > 0$ for any vector $\mathbf{A}$ that represents a circle or a line, so $\mathbf{P}$ is good, too.

Thus in the singular case, the eigenvector $\mathbf{A}$ corresponding to $\boldsymbol{\eta} = 0$ is the solution of the constrained minimization problem (5.62)--(5.63).

**Summary.** We conclude that the problem (5.62)--(5.63) can be solved in two steps: first we find all solutions $(\boldsymbol{\eta}, \mathbf{A})$ of the generalized eigenvalue problem (5.68), and then we pick the one with the minimal nonnegative $\boldsymbol{\eta}$. If $\boldsymbol{\eta} = 0$, then the method returns a perfect fit (an interpolating circle or line).

## 5.12 A real data example

Here we present an example of fitting circular arcs to plotted contours in archaeological field expeditions [44]. It was already mentioned in our Preface.

A common archaeological problem consists of estimating the diameter of a potsherd from a field expedition. The original diameter at specific point along the profile of a broken pot --- such as the outer rim or base --- is restored by fitting a circle to a sherd. Sherd profiles are often traced with a pencil on a sheet of graph paper, which is later scanned and transformed into an array of pixels (data points). A typical digitized arc tracing a circular wheelmade antefix is shown in Fig. 5.9. This image contains 7452 measured points.

![](img/86db288e3c266985d1648282179ae4b5_163_0.png)

The best fitting circle found by the geometric (Levenberg-Marquardt) method has parameters

center $= (7.4487, 22.7436)$,     radius $= 13.8251$, (5.71)

which we assume to be exact (ideal).

Fig. 5.10 shows a fragment of the above image, it consists of merely $n = 22$ randomly chosen points (from the original 7452 points). Visually, they do not really appear as a circular arc, they rather look like a linear segment. Surprisingly, geometric fitting algorithms (again, we used the Levenberg-Marquardt) applied to these 22 points returned the following circle:

center = (7.3889, 22.6645),   radius = 13.8111,   (5.72)

which is strikingly accurate (compare this to (5.71)).

![](img/86db288e3c266985d1648282179ae4b5_164_0.png)

Figure 5.10: A fragment of the arc shown in Fig. 5.9.

Now algebraic circle fits presented in this chapter produced the following results:

- center = (10.8452, 19.1690),   radius = 8.9208   (Kåsa)
- center = (11.2771, 18.7472),   radius = 8.3222   (GGS)
- center = (7.3584, 22.6964),   radius = 13.8552   (Nievergelt)
- center = (7.3871, 22.6674),   radius = 13.8146   (Pratt)
- center = (7.3871, 22.6674),   radius = 13.8145   (Taubin)

We see that the Kåsa and Gander-Golub-Strebel (GGS) fits greatly underestimate the radius, while the Nievergelt method overestimates it. The Pratt and Taubin fits are nearly identical and give results very close to the geometric fit. Overall, the Pratt fit found a circle closest to the ideal one (5.71).

One may naturally want to estimate errors of the returned values of the circle parameters, but this is a difficult task for most EIV regression problems, including the circle fitting problem. In particular, under the standard statistical models described in Chapter 6, the estimates of the center and radius of the circle by the Levenberg-Marquardt, Pratt, and Taubin methods happen to have infinite variances and infinite mean values!

An approximate error analysis developed in Chapter 7 can be used to assess errors in a realistic way. Then the errors of the best methods (Levenberg-Marquardt, Pratt, and Taubin) happen to be $\approx 0.1$. For the Kåsa fit, there is an additional bias that needs to be taken into account, too. Since our data point span an arc of ~20°, the Kåsa fit tends to return radius 2-3 times smaller than the actual radius; see Table 5.4. A detailed errors analysis is given in the next two chapters.

## 5.13 Initialization of iterative schemes

In the previous sections we treated each algebraic fit as a stand-alone procedure that aimed at the ultimate goal: an accurate estimation of the true circle parameters. However, in many applications a noniterative algebraic fit is used as an intermediate tool, to merely initialize a subsequent geometric fit.

In that case it is desirable that the algebraic prefit returns an estimate that lies close to the global minimum of the objective function, so that the geometric fit would quickly converge to it. This goal is different from the usual one — closeness to the true parameter value; see an illustration in Fig. 5.11.

![](img/86db288e3c266985d1648282179ae4b5_165_0.png)

Figure 5.11 Minimization of a function F(x). Here a denotes the global minimum, b the true parameter value, and c and d are two different initial guesses. The guess d is closer to the true parameter value, thus it is better than c as a stand-alone estimate. However, c is closer to the minimum a, thus the iterative algorithm starting at c will converge to a faster than the one starting at d.

**Various initialization schemes**. Recall that we have several geometric fitting procedures (Levenberg-Marquardt, Späth, Landau, all described in Chapter 4); theoretically they minimize the same objective function, (4.18), thus ideally they should return the same estimate.

However, in practice they behave quite differently (even if supplied with the same initial guess), because they choose different routes to the minimum. Hence some of them may be trapped in a local minima, some others may move too slowly and stall before reaching the global minimum, etc.

In addition, we have several algebraic fits which may supply different initial guesses to the geometric fitting procedures. We emphasize that each algebraic fit minimizes its own objective function, thus their results differ even theoretically.

Now one can combine any algebraic prefit (such as Kåsa, Pratt, Taubin) with any subsequent geometric fitting routine (such as Levenberg-Marquardt,
