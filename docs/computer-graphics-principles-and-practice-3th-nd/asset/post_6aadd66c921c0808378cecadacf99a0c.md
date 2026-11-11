
## Chapter 24: Implicit Representations of Shape

### 24.1 Introduction

We introduced implicit functions in Chapters 7 and 14 as a means for defining shapes. Implicitly defined shapes, like the circle defined by $x^2 + y^2 = 1$, or the sphere defined by $x^2 + y^2 + z^2 = 1$, or far more general shapes defined by equations of the form $F(P) = c$ for some complicated function $F$, serve several roles in graphics. First, for a wide class of functions, computing ray-surface intersections with such shapes is fairly easy. Second, it’s sometimes convenient to represent surfaces like “the boundary between water and air” in a simulation implicitly, because it’s very easy to change the topology of an implicitly defined surface (by changing either $F$ or $c$), while it’s generally difficult to do so for parametrically defined surfaces. Third, in many applications we find ourselves with data defined on a grid of points (the temperature at each point in a nuclear reactor, for instance, or the material density at each point in a CAT scan of a brain) and we wish to visualize this data; often, seeing the level surface (the set of points where the function has a particular value) for a function that’s consistent with the observed data can help us understand the data. In this chapter, we introduce implicit curves and surfaces and discuss how they are used to model shapes, how they can be used in ray tracing and animation, and how they can be converted to polyhedral meshes.

The main advantages of implicit representations are the general smoothness of the shapes defined this way, the simplicity of creating quite general shapes, the ease of defining shapes whose topology changes over time, and the ability to exactly compute surface normals and other geometric properties (many of which are difficult to estimate for polyhedral surfaces). The disadvantages are that converting an implicit representation to a polygon mesh suitable for most renderers can be very expensive, and that the ability of implicits to represent multiple topologies can also make it difficult to *control* the topology of an implicitly defined shape.

![](img/f464cd0043eb5336aa0543fe20a0561b_666_0.png)

*Figure 24.1. Two implicit curves in the plane. (a) The circle is defined by $x^2 + y^2 = 1$, or by $x^2 + y^2 - 1 = 0$. (b) The lemniscate of Bernoulli is defined by $(x^2 + y^2)^2 = 2c(x^2 - y^2)$; changing $c$ adjusts the angle at which the lines cross at the center of the figure eight.*

### 24.2 Implicit Curves

In Chapter 7 we discussed two ways to describe a line in the plane: either *parametrically* (writing $P + t d$, for values $t ∈ ℝ$) or *implicitly* (in a form like $Ax + By + C = 0$, with $A$ and $B$ not both zero; or in vector form, $(X - P) · n = 0$, where $n$ is a nonzero vector in the plane and $P$ is a point of the line—the set of points $X$ satisfying this equation forms a line containing $P$ and perpendicular to $n$). In addition, we observed that it was particularly easy to find the intersection of a parametric line with an implicit line. Similarly, in 3-space we could define a plane implicitly, and ray-plane intersections were easiest when the ray was parametric and the plane implicit.

We further generalized to talk about implicitly defined curves in the plane that were more general than lines, like the circle, defined by $x^2 + y^2 = 1$, or more general curves (see Figure 24.1). More generally, if we have any function $z = F(x,y)$ defined on the plane,¹ such as the height of the terrain at each location $(x,y)$ in some hilly area, then the sets of points defined by $F(x,y) = c$ are called **contour lines** and are an example of a level set of a function (in the sense that they are the points at the same level on the graph of $F$). Level sets are sometimes also called **isocontours** of $F$. Mathematics books often discuss level sets by only considering the case $c = 0$; that's because the level set where $F(x,y) = c$ is the level set where $G(x,y) = 0$ if we define the function $G$ by

$$G(x,y) = F(x,y) - c.  (24.1)$$

Thus, you'll sometimes encounter the term **zero set** rather than “level set.”

Because the points of the curve are defined indirectly—we simply have the function $F$ which tells us whether a point is on the curve or not—we also say that the curve is an **implicit curve**. If the formula for $F$ is sufficiently complicated, it may not even be clear whether the set defined by $F(x,y) = c$ is empty or not.

In the cases we've discussed so far—the line, circle, and lemniscate—the first two implicit curves are very smooth, but the third has a self-crossing. The distinction among them is the nature of the functions defining them. In general, if $C$ is the level set $F(x, y) = c$, then $C$ consists of disjoint simple closed curves *if* at every point $P$ of $C$, the gradient $\nabla F(P)$ is nonzero.

In the case of the line, the function $F_L(x, y) = Ax + By + C$ has gradient $\nabla F_L(x, y) = \begin{bmatrix} A \\ B \end{bmatrix}$, which is nonzero everywhere. For the circle, the function $F_C(x, y) = x^2 + y^2$ has gradient $\begin{bmatrix} 2x \\ 2y \end{bmatrix}$, which is zero only at $(x, y) = (0, 0)$, which is not a point of the circle. But for the lemniscate,² where

$$F_B(x,y) = (x^2 + y^2)^2 - 2c(x^2 - y^2), \tag{24.2}$$

we have

$$\nabla F_B(x,y) = \begin{bmatrix} 4x(x^2 + y^2) - 4cx \\ 4y(x^2 + y^2) + 2cy \end{bmatrix}, \tag{24.3}$$

which, at $(x, y) = (0, 0)$, is the zero vector. At places where the gradient is zero, an implicit curve can have singularities (self-intersections, sharp corners, tangencies). This is not, however, an if-and-only-if condition. For instance, the circle can also be defined by the equation

$$F(x,y) = ((x^2 + y^2) - 1)^2 = 0, \tag{24.4}$$

which has gradient zero at every point of the circle. In short, a nonzero gradient ensures that the curve is nice, but the curve's niceness tells us nothing about the gradient.

The preceding example also shows that the function that defines an implicit curve is by no means unique: Many functions can define the same curve. That's another drawback of implicits.

How common are zeroes in the gradient? A back-of-the-envelope argument says they're fairly common. If we set the first term of the gradient to zero, we've got one equation in two variables (which defines a curve in the plane); if we set the second to zero as well (defining a second curve in the plane), we've got two equations in two variables. If they were *linear* equations, we'd generally have a solution; because they may be nonlinear, we can merely say that we might well expect to find isolated solutions to the two equations (i.e., points where the two curves intersect). If we chose a level $c$ at random, we would not expect $F(x,y) = c$ to hit any of these gradient zeroes, but if we were to vary $c$, we might well expect that for certain values of $c$, the level set for $c$ contains a gradient zero. This can be thought of in terms of a physical analogy, as shown in Figure 24.2: If we take our function to be the height of the terrain above or below sea level, then when the sea level is $c$, the level set for $c$ is the shoreline. As the tide rises, $c$ changes, and the shape of the shoreline changes. For example, two adjacent islands may be separated by water at high tide (so that the level set consists of two closed curves—the shorelines of each island); as the tide drops, the islands may become joined by an isthmus so that at low tide, the shoreline is one long curve. For some value of $c$, the level set changes from two curves to one curve; at the point where the curves join, the gradient is zero.

![](img/f464cd0043eb5336aa0543fe20a0561b_668_0.png)

Figure 24.2: A topographical map and side view of two islands. At high tide (two almost-circular red curves) the islands are separated and the shoreline has two parts; at low tide (large blue curve) the islands are joined by an isthmus, and the shoreline is a single curve. At mid-tide (green figure-eight curve), the shoreline has a singular point, where the gradient of the height function is zero. In both figures, the faint gray arrows are scaled versions of the gradient of the implicit function.

The gradient of an implicit curve, when nonzero, has another important function: It always points in the direction of the normal vector to the curve. (This, and the claim that when the gradient is nonzero the curve is smooth, are consequences of the implicit function theorem [Spi65].) We can see this in the case of the unit circle: At the point $(x,y)$, the gradient is $\begin{bmatrix}2x\\2y\end{bmatrix}$, which is indeed parallel to the normal, which is $\begin{bmatrix}x\\y\end{bmatrix}$.

We can also see the kinds of problems that arise when the gradient is zero by looking at the function $F(x,y)=1+x^3-y^2$, shown in Figure 24.3 and the level

![](img/f464cd0043eb5336aa0543fe20a0561b_668_1.png)

Figure 24.3: The graph of $F(x,y)=1+x^3-y^2$ and its associated level curves for $c=.95$, $1$, and $1.05$. The level curve for $c=1$ has a cusp at the origin, where the gradient is zero. This example shows that the topology of the level set need not change at a place where the gradient is zero.
