The three parameters $(\rho, d, \phi)$ completely (and uniquely) describe the circular arc. They are convenient in the high energy physics experiments, as they never have to take dangerously large values, and they represent exactly the quantities of practical interest.

**Conversion formulas.** We refer to the illustration in Fig. 8.6, where both $\rho$ and $d$ are positive (other cases are treated similarly). Observe that the line joining the origin with the nearest point on the arc also passes through the circle's center.

Now given $(\rho, d, \phi)$ one can compute the traditional parameters by $R = 1/|\rho|$ and

$$a = (d + \frac{1}{\rho}) \sin \phi \quad \quad \text{and} \quad \quad b = -(d + \frac{1}{\rho}) \cos \phi. \qquad\qquad (8.31)$$

Conversely, given $(a, b, R)$ one can compute the new parameters by $\rho = \pm 1/R$ and by solving the following two equations for $d$ and $\phi$, respectively:

$$(d + \frac{1}{\rho})^2 = a^2 + b^2, \quad \quad \tan \phi = -a/b.$$

**Karimäki's objective function.** To construct his objective function, Karimäki approximates distances between data points $(x_i, y_i)$ and the circle $(a, b, R)$ following an earlier work by Chernov and Ososkov [45]. Namely, he approximates the geometric distance

$$\varepsilon_i = \sqrt{(x_i - a)^2 + (y_i - b)^2} - R$$

by

$$\varepsilon_i \approx \varepsilon_i = (2R)^{-1} \left[ (x_i - a)^2 + (y_i - b)^2 - R^2 \right].$$

He calls this a “highly precise approximation” [107]; we refer to Section 5.4 for the motivation and related discussion.

Then Karimäki expresses the above approximate distance in terms of his circle parameters $(\rho, d, \phi)$:

$$\varepsilon_i = \frac{1}{2} \rho r_i - (1 + \rho d) r_i \sin (\phi - \theta_i) + \frac{1}{2} \rho d^2 + d, \qquad\qquad (8.32)$$

where $r_i$ and $\theta_i$ are the polar coordinates of the $i$th data point, i.e.

$$x_i = r_i \cos \theta_i \quad \quad \text{and} \quad \quad y_i = r_i \sin \theta_i.$$

Next Karimäki rewrites (8.32) as

$$\varepsilon_i = (1 + \rho d) \left( \kappa r_i^2 - r_i \sin (\phi - \theta_i) + \mu \right), \qquad\qquad (8.33)$$

where

$$\kappa = \frac{\rho}{2(1 + \rho d)} \quad \quad \text{and} \quad \quad \mu = \frac{1 + \frac{1}{2} \rho d}{1 + \rho d} d, \qquad\qquad (8.34)$$