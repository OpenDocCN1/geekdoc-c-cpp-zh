on the desired circle. Then one uses that point as the pole of the inversion transformation. The big question is how to find such a point.

**The choice of a pole.** Assuming that all the data points are close to the desired circle, one can use any one of them as the pole, i.e., select $i=1,\ldots, n$ and set $(x_{0},y_{0}) = (x_{i},y_{i})$. In most cases this would be a good approximation to a point lying on the desired circle. Such approximations are employed in some realizations [159]. Then one can find a better point on the desired circle by using an iterative scheme; see Section 8.7.

Choosing one of the data points as a pole has its drawbacks. First, that point will be transformed by the inversion to $\infty$, thus its image cannot be used at Step 2, i.e., the sample is effectively reduced. Moreover, nearby data points will be mapped far away from the origin, their new coordinates $(x',y')$ may be very inaccurate (to the extent that they may cause more trouble than good).

In fact, a more stable version of the fit (described in Section 8.6) requires assigning weights to data points and applying a weighted least squares fit at Step 2. The weights must be very small (close to zero) for points near the pole, hence their influence on the fitting circle is strongly suppressed. This effectively reduces the sample size even further.

![](bbox=[0.29, 0.43, 0.76, 0.59])

In some applications a point on the desired circle may be known from the nature of the data. In high energy physics, experimenters commonly deal with elementary particles created (born) in a collision of an energetic particle with a target. The energetic (primary) particle moves in a beam driven by magnetic fields in an accelerator; the new (secondary) particles move along circular arcs (called *tracks*) emanating from the point of collision (called *the vertex*); see a typical picture in Fig. 8.3. The location of the vertex is often known very precisely, then one can fit circular arcs to individual tracks using the coordinates of the vertex.

**A modification of the inversion-based fit.** In some high energy physics experiments the tracks do not exactly pass through the known vertex, and their deviation from the vertex is an important parameter $\varepsilon$, called the *impact of the track*.