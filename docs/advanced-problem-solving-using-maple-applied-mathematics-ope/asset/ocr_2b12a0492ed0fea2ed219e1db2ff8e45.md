> s₁[1..3];
> **Optimum** := eval(V(x), s₁);
> [x₁ = 1904.761905, x₂ = 2380.952381, x₃ = 714.285714]
> 1.880952381 × 10⁶

Check the Hessian.

> H := Student:-VectorCalculus:-Hessian(V(x), [x₁, x₂, x₃]);

$$
H = \begin{bmatrix}
0.40 & 0.10 & 0.04 \\
0.10 & 0.16 & 0.06 \\
0.04 & 0.06 & 0.36
\end{bmatrix}
$$

The Hessian matrix $H$ has all positive leading principal minors. Therefore, since $H$ is always positive definite, then our solution is the optimal minimum. The expected return is 12.0% found from $g_1(x)/5000 = (0.14 \cdot 1904.8 + 0.11 \cdot 2381 + 0.10 \cdot 714.2)/5000$.

# Exercises

+   1. Solve the following constrained problems using the Kuhn-Tucker Conditions (KTC) approach.
+   
+   (a) Minimize $z=x^2+y^2$ subject to $x+2y=4$.
+   
+   (b) Maximize $z=(x-3)^2+(y-2)^2$ subject to $x+2y=4$.
+   
+   (c) Maximize $z=x^2+4xy+y^2$ subject to $x^2+y^2=1$.
+   
+   (d) Maximize $z=x^2+4xy+y^2$ subject to $x^2+y^2=4$ and $x+2y=4$.

+   2. Maximize $Z=3X^2+Y^2+2XY+6X+2Y$ subject to $2X-Y=4$.
+      Did you find the maximum? Explain.

+   3. Two manufacturing processes, $f_1$ and $f_2$, both use a resource with $b$ units available. Maximize $f_1(x_1)+f_2(x_2)$ subject to $x_1+x_2=b$.
+   
+   If $f_1(x_1)=50-(x_1-2)^2$ and $f_2(x_2)=50-(x_2-2)^2$, analyze the manufacturing processes using the KTC approach.
+   
+   (a) determine the amount of $x_1$ and $x_2$ to use to maximize $f_1+f_2$;
+   
+   (b) determine the amount $b$ of the resource to use.

+   4. Use the Kuhn-Tucker Conditions to find the optimal solution to the following nonlinear problems.
+   
+   (a) Maximize $f(x,y)=-x^2-y^2+xy+7x+4y$ subject to $2x+3y\geq16$ and $-5x+12y\leq20$.