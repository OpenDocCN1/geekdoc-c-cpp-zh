3. Since the 1st order leading principal minors are negative and the 2nd order is positive, the Convexity and the Hessian Matrix theorem tells us that $g$ is a concave function.

[Figure 4.3](#) shows $g$'s graph.

![](bbox=[0.291, 0.269, 0.669, 0.487])

**FIGURE 4.3:** Graph of $g(x_1,x_2)=-x_1^2-3x_2^2+x_1x_2$

# **Example 4.6. Determining Nonconvexity Using the Hessian.**

Determine the convexity of the function $h(x_1,x_2)=x_1^2-3x_2^2+x_1x_2$ using its Hessian matrix.

+   1. The Hessian of $h$ is
+   
+   $$
+   H(h)=\begin{bmatrix}
+   \frac{\partial^2h}{\partial x_1^2} & \frac{\partial^2h}{\partial x_1\partial x_2}\\
+   \frac{\partial^2h}{\partial x_1\partial x_2} & \frac{\partial^2h}{\partial x_2^2}
+   \end{bmatrix}
+   =\begin{bmatrix}2 & 1\\1 & -6\end{bmatrix}
+   $$

+   2. The 1st order leading principal minors are: $|2|=2>0$ & $|-6|=-6<0$.
+   
+   Stop. Since we have opposite signs, $h$ cannot be either convex or concave; $h$ has a saddle point.

The function is neither convex nor concave; this Hessian matrix is called *indefinite*.