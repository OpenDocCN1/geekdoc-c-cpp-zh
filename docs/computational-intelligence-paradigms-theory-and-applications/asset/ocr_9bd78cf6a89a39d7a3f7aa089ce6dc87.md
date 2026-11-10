+   1. Step 1: Present the input vectors to the ANFIS model.
+   2. Step 2: Compute the node outputs of each layer.
+   3. Step 3: Repeat Step 2 for all the presented input signal.
+   4. Step 4: Compute the consequent parameters using the LSE algorithm.
+   5. Step 5: Compute the error measure for each training pair.

# Backward Pass: Steepest Descent Method

Though the steepest descent method is one of the oldest methods, it is best suitable for solving constrained as well as unconstrained problems. This method is a most frequently used nonlinear optimization technique.

Let $z=f(\vec{X})$ be a function of $\vec{X}$ such that $\frac{\partial f(\vec{X})}{\partial x_k}$ exists for $k=1,2,\ldots,n$. The gradient of $f(\vec{X})$, denoted by $\nabla f(\vec{X})$, is the vector $\nabla f(\vec{X})=\left[\frac{\partial f(\vec{X})}{\partial x_1},\frac{\partial f(\vec{X})}{\partial x_2},\ldots,\frac{\partial f(\vec{X})}{\partial x_n}\right]^T$.

The direction of the gradient points to the local steepest downhill direction at the greatest rate of increase of rate of $f(\vec{X})$. Therefore $-\nabla f(\vec{X})$ points in the direction of steepest decrease of $f(\vec{X})$. An iterative search procedure is performed, starting from point $\vec{P}_0$ in the direction $\vec{S}_0=-\frac{\nabla f(\vec{P}_0)}{\|\nabla f(\vec{P}_0)\|}$. Upon this search a point $\vec{P}_1$ is obtained at which the local minimum occurs according to the relation $\vec{X}=\vec{P}+\nu\vec{S}_0$. This search and minimization continues to produce a sequence of points with the property $f(\vec{P}_0)>f(\vec{P}_1)>\ldots>f(\vec{P}_k)=P$, then $f(P)$ will be a local minimum.

The basic algorithm of the steepest descent search method is given as follows:

+   1. Step 1: Evaluate the gradient vector $\nabla f(P_k)$.
+   2. Step 2: Calculate the direction of search $\vec{S}_k=-\frac{\nabla f(P_k)}{\|\nabla f(P_k)\|}$.
+   3. Step 3: Execute a single parameter minimization of $g(\nu)=f(P_k+\nu\vec{S}_k)$ on the interval $[0,b]$. Upon execution of $g(\nu)=h_{min}$ is produced at which the local minimum for $g(\nu)$ lies. The relation $g(\nu)=f(P_k+h_{min}\vec{S}_k)$ shows that this is a minimum for $f(\vec{X})$ along the search line $\vec{X}=P_k+\nu\vec{S}_k$.
+   4. Step 4: Search for the next point $P_{k+1}=P_k+h_{min}\vec{S}_k$.
+   5. Step 5: Test for termination condition.
+   6. Step 6: Repeat the entire process.