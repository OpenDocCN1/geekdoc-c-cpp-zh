![](bbox=[0.177, 0.091, 0.824, 0.291])

**FIGURE 3.6** There exists a *linear correspondence* between the user coordinates $(x_i,y_i)$ (on the left) and the *canvas coordinates* $(\bar{x}_i,\bar{y}_i)$ (on the right).

Considering, in particular for the $x$-axis, that the limits $x_{\min}$ and $x_{\max}$ of the user domain can be determined from the set of arguments $x_i$, and that the limits $\bar{x}_{\min}$ and $\bar{x}_{\max}$ of the canvas domain are set independently, in accordance with the desired positioning of the plot, the scaling coefficients $A_x$ and $B_x$ can be determined from the linear conditions:

$$\bar{x}_{\min}=A_xx_{\min}+B_x,$$

$$\bar{x}_{\max}=A_xx_{\max}+B_x,$$

wherefrom, the scaling coefficients for the $x$-axis are

$$A_x=(\bar{x}_{\max}-\bar{x}_{\min})/(x_{\max}-x_{\min})$$

$$B_x=\bar{x}_{\min}-A_xx_{\max}.$$ 

(3.1)

Analogously, the scaling coefficients $A_y$ and $B_y$ for the $y$-axis are given by

$$A_y=(\bar{y}_{\max}-\bar{y}_{\min})/(y_{\max}-y_{\min})$$

$$B_y=\bar{y}_{\min}-A_yy_{\min}.$$ 

(3.2)

There exists, though, a lack of symmetry between the $x$- and $y$-axes. This difference stems, on the one hand, from the fact that, while the set of arguments $x_i$ is supposed to be ascendingly ordered, with $x_{\min}$ and $x_{\max}$ coinciding, respectively, with $x_1$ and $x_n$, the set of ordinates $y_i$ is not necessarily ordered (except for the case of monotonic functions), and hence, the limiting values $y_{\min}$ and $y_{\max}$ have to be explicitly determined. On the other hand, since the vertical axes in user and canvas coordinates have opposite directions, ascending canvas $y$-coordinates actually decrease (down to $0$) for increasing $y$-coordinates.

With the scaling coefficients given by Equations 3.1 and 3.2, the canvas coordinates corresponding to the $n$-tabulated function values are determined from the relations:

$$\bar{x}_i=A_xx_i+B_x,\quad i=1,2,\ldots,n$$

$$\bar{y}_i=A_yy_i+B_y.$$

The minimal Python graphics library `graphlib0.py` presented in Listing 3.7 is meant to illustrate the basic concepts underlying scientific graphics, by providing elementary functionalities for plotting