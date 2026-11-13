The next question is how to actually compute these separatrices. To do this, we first observe that saddle points are a special case of all critical points shown in Figure 6.31: At a saddle point, exactly four separatrices meet. It can also be shown that, at a saddle point, separatrices are tangent to the two eigenvectors of J, and that the outgoing and incoming separatrices are tangent to the eigenvectors having positive, respectively negative, Re components [Helman and Hesselink 89].

The algorithm for computing separatrices from a given 2D field thus can proceed by linking saddle points to other streamline endpoints, as follows:

+   1. Compute and classify all critical points following Figure 6.31.
+   2. For all saddle points s, start tracing two streamlines in the directions of their eigenvectors having positive Re values.
+   3. Stop tracing when the streamline hits the boundary of D or another critical point where ||v|| = 0.
+   4. Merge curves that start and end between the same endpoints.

The output of this algorithm is a graph whose nodes are critical points or points where streamlines leave the computational domain, and edges are the respective separatrices. Figure 6.30(d) shows the result for the vector field illustrated earlier.

Robust implementation of the above algorithm, however, requires several preceptions, as follows.

Interpolation issues: Detecting critical points firstly needs finding locations where ||v|| = 0. However, the vector field v is usually point-sampled on a discrete grid. As such, we must use interpolation of cell vertex values to find the exact points where the magnitude of v vanishes. To do this, we can use the interpolation mechanisms presented in Chapter 3. The same interpolation mechanisms must be used to estimate the components of the Jacobian matrix J at the detected critical points (see Section 3.7).

Excluding critical points: Several critical points are usually excluded from computing separatrices. First, center points are typically eliminated, since they do not contribute to global information on the topology of a vector field, but only describe small-scale local circular (vortex-like) areas. Second, since all our computations are done using interpolated data, the conditions on the real and imaginary components of eigenvalues of the Jacobian J (Figure 6.31) are naturally subject to numerical errors. In practice, these conditions are relaxed to