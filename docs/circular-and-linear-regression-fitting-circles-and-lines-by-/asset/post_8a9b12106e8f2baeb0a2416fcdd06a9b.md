
points, and the noise level $\sigma^2$ is unknown and we are estimating it, too. Denote by $\hat{A}_n, \hat{B}_n, \hat{C}_n, \hat{\sigma}^2_n$ the estimators of these parameters.

Let $\mathfrak{E}$ denote the class of all estimators $\hat{A}_n, \hat{B}_n, \hat{C}_n, \hat{\sigma}^2_n$ which are consistent and asymptotically normal, with the asymptotic covariance matrix depending on the sequence of the true points $(\tilde{x}_i, \tilde{y}_i)$ only through their limit values $\bar{x}_s, \bar{y}_s$, and $s_s$. Then within $\mathfrak{E}$, the maximum likelihood estimators of $A, B, C$ and the estimator (2.27) of $\sigma^2$ are the best estimators, i.e., they have the asymptotically smallest possible covariance matrix.

This remarkable result is due to Gleser [74, 75], see also Cheng and Van Ness [38, 39, 40].

**Final remarks.** This concludes our brief summary of the orthogonal line fitting. We have covered only selected aspects of this subject, which seemed to be most relevant to our main objectives — fitting circles and ellipses. We left out nonorthogonal EIV linear regression, multidimensional linear regression, structural and ultra-structural models, and many other interesting but not quite relevant topics.

## Chapter 3

## Fitting circles: Theory

- 3.1 Introduction 47
- 3.2 Parametrization 48
- 3.3 (Non)existence 53
- 3.4 Multivariate interpretation of circle fit 55
- 3.5 (Non)uniqueness 57
- 3.6 Local minima 59
- 3.7 Plateaus and valleys 61
- 3.8 Proof of Two Valley Theorem 64
- 3.9 Singular case 67

### 3.1 Introduction

**Variety of applications.** The need of fitting circles or circular arcs to observed points arises in many areas. In medicine, one estimates the diameter of a human iris on a photograph [141] or designs a dental arch from an X-ray [21]. Archaeologists examine the circular shape of ancient Greek stadia [157] and mysterious megalithic sites (stone rings) in Britain [65, 177]; in other studies they determine the size of ancient pottery by analyzing potsherds found in field expeditions [44, 80, 81, 190]. In industry, quality control requires estimation of the radius and the center of manufactured mechanical parts [119] (other interesting applications involve microwave engineering [54, 169] and the lumber industry [13]).

In nuclear physics, one deals with elementary particles born in an accelerator — they move along circular arcs in a constant magnetic field; physicists determine the energy of the particle by measuring the radius of its trajectory; to this end experimenters fit an arc to the trace of the electrical signals the particle leaves in special detectors [53, 45, 106]. In mobile robotics, one detects round objects (pillars, tree trunks) by analyzing range readings from a 2D laser range finder used by a robot [197]. In computer vision, one uses a sequence of arcs “stitched together” (a “circular spline”) to approximate more complex curved shapes [12, 145, 158, 164, 165].

**Different practical requirements.** All these applications involve fitting circles to planar images, but the character of data and the requirements may differ widely. In some cases one deals with data points sampled along a full circle (like in a human iris image or a log in lumber industry). In other cases the data are badly incomplete — one observes just a small arc of a big circle.

In some applications (e.g., in medicine) the fit must be very accurate and the computational cost is not an issue. Others are characterized by mass data processing (for instance, in high energy physics, millions of particle tracks per day can be produced by an accelerator), and the processing speed is of paramount importance. These variations certainly dictate different approaches to the fitting problem, as we will see below.

## 3.2 Parametrization

**Standard parameters.** To fit a circle to observed points { $(x_i, y_i)$ } by orthogonal least squares one minimizes the sum of squares

$$ \mathscr{F} = \sum_{i=1}^{n} d_i^2, \quad\quad\quad (3.1) $$

where $d_i$ is the (geometric) distance from the data point $(x_i, y_i)$ to the hypothetical circle. The canonical equation of a circle is

$$ (x-a)^2+(y-b)^2=R^2, \quad\quad\quad (3.2) $$

where $(a, b)$ is its center and $R$ its radius; then the (signed) distance is given by

$$ d_i = \sqrt{(x_i-a)^2+(y_i-b)^2} - R. \quad\quad\quad (3.3) $$

Note that $d_i > 0$ for points outside the circle and $d_i < 0$ inside it. Hence

$$ \mathscr{F}(a, b, R) = \sum_{i=1}^{n} \big[\sqrt{(x_i-a)^2+(y_i-b)^2} - R\big]^2. \quad\quad\quad (3.4) $$

**Elimination of R.** This function is just a quadratic polynomial in $R$, hence $\mathscr{F}$ has a unique global (conditional) minimum in $R$, when the other two variables $a$ and $b$ are kept fixed. That conditional minimum can be easily found. If we denote

$$ r_i = r_i(a, b) = \sqrt{(x_i-a)^2+(y_i-b)^2}, \quad\quad\quad (3.5) $$

then the minimum of $\mathscr{F}$ with respect to $R$ is attained at

$$ \hat{R} = \bar{r} = \frac{1}{n}\sum_{i=1}^{n} r_i. \quad\quad\quad (3.6) $$

This allows us to eliminate $R$ and express $\mathscr{F}$ as a function of $a$ and $b$ only:

$$ \begin{aligned} \mathscr{F}(a, b) &= \sum_{i=1}^{n}\left[ r_i - \bar{r} \right]^2 \\ &= \sum_{i=1}^{n}\left[ \sqrt{(x_i - a)^2 + (y_i - b)^2} - \frac{1}{n}\sum_{j=1}^{n} \sqrt{(x_j - a)^2 + (y_j - b)^2} \right]^2 \end{aligned} \quad\quad\quad (3.7) $$

This is still a complicated expression, and it cannot be simplified any further. The minimization of (3.7) is a nonlinear problem that has no closed form solution.

The little advantage of (3.7) over (3.4) is that a function of two variables, $\mathscr{F}(a, b)$, can be easily graphed and examined visually (which we will do below), while for a function $\mathscr{F}(a, b, R)$ such a visual inspection is difficult.

![](img/86db288e3c266985d1648282179ae4b5_82_0.png)

Figure 3.1 Data points (diamonds) are sampled along a very small arc of a big circle. The correct fit (the solid line) and the wrong fit (the dashed line) have centers on the opposite sides of the data set.

In this chapter we discuss theoretical properties of the objective function $\mathscr{F}$ and its minimum; in the next two chapters we present practical methods of computing the minimum of $\mathscr{F}$. Our first theme is the analysis of various parametrization schemes used in circle fitting applications.

**Drawbacks of the standard parameters.** The geometric parameters $(a, b, R)$ of a circle are standard; they are simple and describe all circles in the plane. There is a problem, however, if one fits circles of very large radii. This may happen when the data are sampled along a small arc (of say less than 5 degrees), see Fig. 3.1; then the radius of the fitted circle can potentially take arbitrarily large values. In that case a small perturbation of data points or a small inaccuracy of the fitting procedure may result in the circle center being on the “wrong side” (see the dashed arc in Fig. 3.1).

In addition, numerical computations become unreliable: a catastrophic loss of accuracy may occur when two large nearly equal quantities are subtracted in (3.3). We call this a *problematic*, or a *singular case* of a circle fit. We will see shortly that in this case even more serious problems arise than catastrophic cancellations.

![](img/86db288e3c266985d1648282179ae4b5_83_0.png)

**Karimäki’s parameters.** If experiments where incomplete arcs (partially occluded circles) are frequent, statisticians often adopt different parametrization schemes. For example, in nuclear physics Karimäki [106] proposes to replace $R$ with a signed curvature $\rho = \pm R^{-1}$ and the center $(a, b)$ with the distance of the closest approach ($d$) to the origin, and the direction of propagation ($\phi$) at the point of closest approach, see Fig. 3.2. We will describe these parameters more precisely in Section 8.8. The three parameters ($\rho, d, \phi$) completely (and uniquely) describe the fitting circular arc, and they never have to take dangerously large values (unless $R \approx 0$, hence $\rho \approx \infty$, which is actually not a bothersome event).

Karimäki’s parameters have a clear geometric meaning, but expressing the objective function $\mathcal{F}$ in terms of $(\rho, d, \phi)$ leads to cumbersome formulas; see [106] and our Section 8.8. Another pitfall in Karimäki’s scheme is that for circles centered on the origin, the direction $\phi$ becomes indeterminate. If the center of the fitting circle gets close to the origin, numerical algorithms cannot handle the $\phi$ parameter adequately and may get stuck.

**Algebraic parameters.** A more elegant scheme was proposed by Pratt [150] and others [67], which describes circles by an algebraic equation,

$$ A(x^{2} + y^{2}) + Bx + Cy + D = 0 \tag{3.8} $$

with an obvious constraint $A \neq 0$ (otherwise this equation describes a line) and a less obvious constraint

$$ B^{2} + C^{2} - 4AD > 0. \tag{3.9} $$
