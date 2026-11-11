you can easily convert between them. If we have two lines whose intersection we need to compute, we could do an implicit-implicit, parametric-parametric, or parametric-implicit computation. The implicit-implicit version is messy enough that it’s better to convert one line to parametric form and use the implicit-parametric intersection approach. We’ll begin by computing the intersection of two lines in parametric form, mostly so that you see the benefit of the later implicit-parametric form. In general, we find that intersections between implicit and parametric forms tend to produce the simplest algebra.

# 7.7.1 Parametric-Parametric Line Intersection

Suppose we have two lines in parametric form, that is, two functions

$$\gamma : \mathbb{R} \to \mathbb{R}^2 : t \mapsto tA + (1-t)B, \tag{7.72}$$

$$\eta : \mathbb{R} \to \mathbb{R}^2 : s \mapsto sC + (1-s)D, \tag{7.73}$$

whose images are (respectively) the line $AB$ and the line $CD$ (see Figure 7.13). We’d like to find the point $P$ where these lines intersect. That point will lie on the line determined by $\gamma$, that is, it will be $\gamma(t_0)$ for some real number $t_0$; similarly, it’ll be $\eta(s_0)$ for some real number $s_0$. Equating these gives

![](bbox=[0.711, 0.345, 0.934, 0.448])

$$t_0A + (1-t_0)B = s_0C + (1-s_0)D, \tag{7.74}$$

which can also be written

$$B - D = -t_0(A - B) + s_0(C - D), \tag{7.75}$$

which is a nice form because it involves only vectors (i.e., differences between points).

If we write out Equation 7.74 in terms of the known coordinates of the points $A$, $B$, $C$, and $D$, we get two equations in the two unknowns $s_0$ and $t_0$ and can solve for them. We can then compute $P$ by computing either $t_0A + (1-t_0)B$ or $s_0C + (1-s_0)D$.

An alternative, and preferable, approach is to use the vector form shown in Equation 7.75. Letting $\mathbf{v}=A-B$ and $\mathbf{u}=C-D$, we have

$$B - D = -t_0\mathbf{v} + s_0\mathbf{u}. \tag{7.76}$$

Taking the dot product of both sides with $\times\mathbf{v}$, we get

$$(B-D)\cdot(\times\mathbf{v}) = -t_0\mathbf{v}\cdot(\times\mathbf{v}) + s_0\mathbf{u}\cdot(\times\mathbf{v}) \tag{7.77}$$

$$(B-D)\cdot(\times\mathbf{v}) = s_0\mathbf{u}\cdot(\times\mathbf{v}) \tag{7.78}$$

$$\frac{(B-D)\cdot(\times\mathbf{v})}{\mathbf{u}\cdot(\times\mathbf{v})} = s_0 \tag{7.79}$$

where the simplification arises because $\times\mathbf{v}$ is perpendicular to $\mathbf{v}$, so their dot product is zero. The last trick—eliminating a term from an equation by taking the dot product of both sides with a vector orthogonal to that term—is often useful.

*Figure 7.13: The lines $AB$ and $CD$ are the images of the parametric functions $\gamma$ and $\eta$; they intersect at the unknown point $P$.*