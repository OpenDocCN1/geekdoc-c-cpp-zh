# **8.8 Karimäki fit**

An interesting fitting scheme was developed in 1991 by Karimäki [106, 107] for applications in high energy physics. His scheme is similar, in spirit, to inversion-based fits by Brandon and Cowley [25] and Hansroul, Jeremle, and Savard [82] discussed in Section 8.5. But instead of conformal maps, Karimäki uses a trigonometric change of parameters.

**Karimäki’s parameters.** Recall (Section 8.5) that in nuclear physics experiments, one fits circular arcs to tracks of elementary particles; tracks commonly have a large radius (i.e., a small curvature) and pass near a fixed region in the detector (the vertex). If the origin of the coordinate system is close to the vertex, then the tracks pass near the origin.

In these experiments, the traditional circle parameters $(a, b, R)$ are not convenient as they frequently take large values leading to numerical instability. In the limit of straight line tracks (which are characteristic for particles with very high energy), these parameters turn infinite and the computations fail. This problem was discussed at length in Section 3.2.

Karimäki [106] proposes an alternative set of parameters defined geometrically (by using trigonometric functions). He replaces the radius $R$ with a signed curvature $\rho = \pm R^{-1}$, see below, and the center $(a, b)$ with two other parameters, $d$ and $\phi$, illustrated in Fig. 8.6. He calls $d$ the distance of the closest approach to the origin (i.e., the distance from $(0, 0)$ to the circle), and $\phi$ the direction of propagation at the point of closest approach.

Karimäki’s choice of signs for $\rho$ and $d$ is the following: $\rho > 0$ for tracks turning clockwise and $\rho < 0$ for those turning counterclockwise (at the point closest to the origin); the sign of $d$ is determined from the equation

$$d = x_d \sin \phi - y_d \cos \phi,$$

where $(x_d, y_d)$ is the point of the circle closest to the origin. Our Fig. 8.6 shows a configuration where both $\rho$ and $d$ are positive.

![](bbox=[0.35, 0.67, 0.75, 0.82])

*Figure 8.6: Karimäki’s parameters $d$ and $\phi$.*