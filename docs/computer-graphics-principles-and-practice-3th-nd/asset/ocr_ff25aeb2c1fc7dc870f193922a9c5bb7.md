so we can recover the angle of rotation by computing

$$\theta = \cos^{-1}\left(\frac{\operatorname{tr}(\mathbf{M})-1}{2}\right). \tag{11.25}$$

Two special cases arise at this point, corresponding to the two ways that $\sin\theta$ can be zero.

+   1. If $\theta=0$, then *any* unit vector serves as an “axis” for the rotation, because the rotation is the identity matrix.
+   
+   2. If $\theta=\pi$, then *twice* the rotation has angle $2\pi$, and thus is the identity, that is, our rotation $\mathbf{M}$ must satisfy $\mathbf{M}^2=\mathbf{I}$. From this we find that
+   
+      $$\mathbf{M}(\mathbf{M}+\mathbf{I})=\mathbf{M}^2+\mathbf{M}=\mathbf{I}+\mathbf{M}=\mathbf{M}+\mathbf{I}. \tag{11.26}$$
+   
+      That means that when we multiply $\mathbf{M}$ by $\mathbf{M}+\mathbf{I}$, every column of $\mathbf{M}+\mathbf{I}$ remains unchanged. So any nonzero column of $\mathbf{M}+\mathbf{I}$, when normalized, can serve as the axis of rotation. We know that at least one column of $\mathbf{M}+\mathbf{I}$ is nonzero; otherwise, $\mathbf{M}=-\mathbf{I}$. But this is impossible, because the determinant of $-\mathbf{I}$ is $-1$, while that of $\mathbf{M}$ is $+1$.

In the general case, when $\sin\theta\ne 0$, we can compute $\mathbf{M}-\mathbf{M}^{\mathsf T}$ to get

$$\mathbf{M}-\mathbf{M}^{\mathsf T}=\mathbf{I}+\sin(\theta)\mathbf{J}_{\boldsymbol\omega}+(1-\cos\theta)\mathbf{J}_{\boldsymbol\omega}^{2}\\
(\mathbf{I}^{\mathsf T}+\sin(\theta)\mathbf{J}_{\boldsymbol\omega}^{\mathsf T}+(1-\cos\theta)(\mathbf{J}_{\boldsymbol\omega}^{2})^{\mathsf T}). \tag{11.27}$$

Because $\mathbf{J}_{\boldsymbol\omega}^{\mathsf T}=-\mathbf{J}_{\boldsymbol\omega}$ and $(\mathbf{J}_{\boldsymbol\omega}^{2})^{\mathsf T}=\mathbf{J}_{\boldsymbol\omega}^{2}$, this simplifies to

$$\mathbf{M}-\mathbf{M}^{\mathsf T}=2\sin(\theta)\mathbf{J}_{\boldsymbol\omega}. \tag{11.28}$$

Dividing by $2\sin\theta$ gives the matrix $\mathbf{J}_{\boldsymbol\omega}$, from which we can recover $\boldsymbol\omega$. The code is given in Listing 11.2.

*Listing 11.2: Code to find the axis and angle from a rotation matrix.*

```
void RotationToAxisAngle(
    Mat33 m,
    out Vector3D omega,
    out double theta)
{
// convert a 3x3 rotation matrix m to an axis-angle representation

theta = Math.acos((m.trace()-1)/2);
if (theta is near zero)
{
    omega = Vector3D(1,0,0); // any vector works
    return;
}
if (theta is near pi)
{
    int col = column with largest entry of m in absolute value;
    omega = Vector3D(m[0, col], m[1, col], m[2, col]);
    return;
}
else
{
    mat 33 s = m - m.transpose();
    double x = -s[1,2], y = -s[0,2], z = -s[1,1];
```