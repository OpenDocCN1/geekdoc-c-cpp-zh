# Response Surface Designs

Response surface designs are useful for modeling a curved quadratic surface to continuous factors. If a minimum or maximum response exists inside the factor region, a response surface model can pinpoint it. Three distinct values for each factor are necessary to fit a quadratic function, so the standard two-level designs cannot fit curved surfaces.

The most popular response surface design is the central composite design, illustrated in the figure to the left below. It combines a two-level fractional factorial and two other kinds of points:

+   - *Center points*, for which all the factor values are at the zero (or midrange) value.
+   - *Axial (or star) points*, for which all but one factor are set at zero (midrange) and that one factor is set at outer (axial) values.

The Box-Behnken design, illustrated in the figure on the right below, is an alternative to central composite designs.

One distinguishing feature of the Box-Behnken design is that there are only three levels per factor.

Another important difference between the two design types is that the Box-Behnken design has no points at the vertices of the cube defined by the ranges of the factors. This is sometimes useful when it is desirable to avoid these points due to engineering considerations. The price of this characteristic is the higher uncertainty of prediction near the vertices compared to the central composite design.

Central Composite Design

Box-Behnken Design

![](bbox=[0.18, 0.75, 0.65, 0.82])

![](bbox=[0.66, 0.73, 0.9, 0.8])