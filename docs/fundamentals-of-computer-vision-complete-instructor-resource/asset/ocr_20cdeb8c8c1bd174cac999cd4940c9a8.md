![](bbox=[0.096, 0.118, 0.885, 0.252])

Figure 8.23 The first, on the left, is the initial, showing circular contours. In the second, through the fourth, the level set continues to grow. The authors are grateful to T. F. Chen for this figure. Used with permission. From [8.14].

variation and we want the contour to be smooth. This can be accomplished by using curvature, which tells us how rapidly the contour is changing. The curvature of the level set may be locally determined from

```
\kappa = \frac{\psi_{xx}\psi_y^2 + 2\psi_x\psi_y\psi_{xy} + \psi_{yy}\psi_x^2}{(\psi_x^2 + \psi_y^2)^{3/2}}.
(8.43)
```

If the denominator in this equation is zero, problems occur, and a zero denominator is not impossible, especially for synthetic images. To avoid inconvenience, Eq. 8.43 may be stabilized by adding a small constant to the denominator, a number like 0.01. Remembering that curvature normally only takes on values between zero and one, the behavior we seek can be obtained by using curvature in a way similar to this [8.44]:

```
S_I = 1 - \epsilon\kappa,
(8.44)
```

where $\epsilon$ is a constant used to determine the influence of the curvature, $\kappa$.

There are many ways to define speed that will function in this role. The sign of the speed may be chosen to encourage the contour to move in or out. If we define $S = S_\epsilon S_\epsilon$, Eq. 8.41 becomes

```
\frac{d\psi}{dt} = -S|S_\epsilon|\nabla_k\psi|.
(8.45)
```

Eq. 8.45 is used to update $\psi$ by relating speed to curvature using

```
\psi^{n+1}(x, y) = \psi^n(x, y) - \alpha S(x, y) |\nabla_k \psi(x, y)|,
(8.46)
```

where $\alpha$ is some small scalar. $\alpha$ is used just as in Eq. 3.40 to ensure the algorithm does not step completely over the optimal solution in a single step.

Over the course of running the algorithm, the metric function evolves following a rule like Eq. 8.46. As it evolves, it will have zero values at different points, and those points will define the evolution of the contour, i.e., the zero level set.

In Figure 8.23, four instances in the evolution of a level-set based segmentation are illustrated. The original image is a computed tomographic image of the chest. Dark areas in the chest are being identified.

5 The curvature is 1/(radius of locally best fitting circle). A straight line has infinite radius – zero curvature, and we cannot define a circle smaller than a single pixel.