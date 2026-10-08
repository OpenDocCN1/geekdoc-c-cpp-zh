minimal possible variance, to the leading order; the difference between them
should be then characterized in terms of their biases, to which we turn next.

The essential bias of the Pratt fit is, due to (7.42),

$\mathbb{E}(\Delta_2 \hat{\Theta}_{\text{Pratt}}) \stackrel{\text{ess}}{=} \frac{2\sigma^2}{\bar{R}} \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}. \quad (7.52)$

Observe that the estimates of the circle center are essentially unbiased, and
the essential bias of the radius estimate is $2\sigma^2/\bar{R}$, which is independent of the
number and location of the true points. We know (Section 7.5) that the essential
bias of the Taubin fit is twice as small, hence

$\mathbb{E}(\Delta_2 \hat{\Theta}_{\text{Taubin}}) \stackrel{\text{ess}}{=} \frac{\sigma^2}{\bar{R}} \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}, \quad (7.53)$

Comparing to (7.10) shows that the geometric fit has an essential bias that is
twice as small as that of Taubin and four times smaller than that of Pratt.

Therefore, the geometric fit has the smallest bias among all the popular
circle fits, i.e., it is statistically most accurate. We observed that fact experi-
mentally in Chapter 5.

**Bias of the Kása fit.** The formulas for the bias of the Kása fit can be de-
river, too, but in general they are complicated. However recall that all our fits,
including Kása, are independent of the choice of the coordinate system, hence
we can choose it so that the true circle has center at $(0,0)$ and radius $\bar{R} = 1$;
this will simplify the formulas. For this circle $\mathbf{\bar{A}} = \frac{1}{\sqrt{2}} [1, 0, 0, -1]^T$, hence
$\mathbf{P}\mathbf{\bar{A}} = 2\mathbf{\bar{A}}$ and so $\mathbf{\bar{M}}^\top \mathbf{P}\mathbf{\bar{A}} = \mathbf{0}$, i.e., the middle term in (7.36) is gone. Also note
that $\mathbf{\bar{A}}^\top \mathbf{P}\mathbf{\bar{A}} = 2$, hence the last term in parentheses in (7.36) is $2\sqrt{2} [1, 0, 0, 0]^T$.
Then observe that $\tilde{z}_i = 1$ for every true point, thus

$\mathbf{M} = \begin{bmatrix} 1 & \bar{x} & \bar{y} & 1 \\ \bar{x} & \overline{xx} & \overline{xy} & \bar{x} \\ \bar{y} & \overline{xy} & \overline{yy} & \bar{y} \\ 1 & \bar{x} & \bar{y} & 1 \end{bmatrix}.$

Next, assume for simplicity that the true points are equally spaced on an arc of
size $\theta$ (which is a typical arrangement in many studies). Choosing the coordi-
nate system so that the east pole $(1,0)$ of the circle is at the center of that arc
ensures $\bar{y} = \overline{xy} = 0$. It is not hard to see now that

$\tilde{\mathbf{M}}^{-1} [1, 0, 0, 0]^T = \frac{1}{4} (\overline{xx} - \bar{x}^2)^{-1} [\overline{xx}, -2\bar{x}, 0, \overline{xx}]^T.$

Using the formula (7.47) we obtain (omitting details as they are not so relevant)