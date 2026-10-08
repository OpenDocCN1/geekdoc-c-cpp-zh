# ADVANTAGES OF THE KÅSA METHOD

Solving this system by some methods of linear algebra (see, e.g., below) gives $B, C, D$, and finally one computes $a, b, R$ by

```
$a = -\frac{B}{2}, \qquad b = -\frac{C}{2}, \qquad R = \frac{\sqrt{B^2 + C^2 - 4D}}{2}$. (5.6)
```

This algorithm is very fast, it can be accomplished in $13n+35$ flops if one solves (5.5) directly. It actually costs less than one iteration of the Gauss-Newton or Levenberg-Marquardt methods (Chapter 4). We note, however, that a direct solution of (5.5) is not the best option; the system (5.5) is an analogue of normal equations that are known to cause numerical instability; a stable solution is described in the next section.

The above algebraic fit has been proposed in the early 1970s by Delogne [54] and Kåsa [108], and then rediscovered and published independently by many authors [11, 24, 25, 36, 51, 53, 125, 129, 136, 170, 180, 193, 197]. Now it is called Delogne-Kåsa method (see [196]) or briefly Kåsa method (see [52, 159, 184]), named after the first contributors. (It seems that most authors prefer the short name “Kåsa method,” so we follow this tradition, too.)

The simplicity and efficiency of the Kåsa algorithm are very attractive features. Many researchers just fall in love with it at first sight. This method is so popular in the computer science community that we feel obliged to present its detailed analysis here. Even though it would not be a method of our choice, we will methodically highlight its strong and weak points.

# 5.2 Advantages of the Kåsa method

The use of Kåsa algorithm actually has many benefits.

First, if the points $(x_i, y_i)$ happen to lie on a circle, the method finds that circle right away. (In contrast, geometric fits would at best converge to that circle iteratively.)

In statistical terms, the Kåsa method is consistent in the small-noise limit $\sigma \rightarrow 0$ (introduced in our discussion in Section 2.5), i.e., the estimates of the parameters $(a, b, R)$ converge to their true values as $\sigma \rightarrow 0$. In fact, the Kåsa fit is asymptotically efficient (optimal) in that limit, to the leading order; see Chapter 7.

**Geometric descriptions.** Second, the Kåsa method can be defined geometrically in several ways. For example, observe that $\pi f_i$, where $f_i$ is given by (5.2), is the difference between the *areas* of two concentric circles, both centered on $(a, b)$: one has radius $R$ and the other passes through the observed point $(x_i, y_i)$, i.e., has radius $r_i = \sqrt{(x_i - a)^2 + (y_i - b)^2}$. In other words, $\pi f_i$ is the area of the ring between the fitted circle and the observed point. Thus the Kåsa method minimizes the combined area of such rings; this interesting fact was noted in [180].