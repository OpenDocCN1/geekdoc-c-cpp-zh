Then, as we will show in the following, $X(t)$ is stationary if and only if $\varphi(1)=\varphi(2)=0$, where $\varphi(u)$ is the characteristic function of $\mathcal{Y}$, that is,

$$\varphi(u)=E[e^{iu\mathcal{Y}}] \qquad \text{for } i=\sqrt{-1}.$$

Before verifying this result we first note that $\varphi(u)$ can be written as

$$\varphi(u)=E[\cos(u\mathcal{Y})]+iE[\sin(u\mathcal{Y})]. \tag{1.12}$$

We will also make use of the trigonometric identities

+   1. $\cos(A+B)=\cos A\cos B-\sin A\sin B$
+   2. $\cos A\cos B=\frac{1}{2}\cos(A+B)+\frac{1}{2}\cos(A-B)$

Using identity (1), we see that $X(t)$ in [Equation 1.11](#) can be expressed as

$$X(t)=C[\cos\lambda t\cos\mathcal{Y}-\sin\lambda t\sin\mathcal{Y}], \tag{1.13}$$

while the product $X(t)X(t+h)$ can be rewritten using first (2) and then (1) as

$$\begin{aligned}
X(t)X(t+h)&=C\cos(\lambda t+\mathcal{Y})C\cos(\lambda(t+h)+\mathcal{Y})\\
&=\frac{C^2}{2}\cos(2\lambda t+\lambda h+2\mathcal{Y})+\frac{C^2}{2}\cos(\lambda h)\\
&=\frac{C^2}{2}[\cos(2\lambda t+\lambda h)\cos(2\mathcal{Y})-\sin(2\lambda t+\lambda h)\sin(2\mathcal{Y})+\cos(\lambda h)]. \tag{1.14}
\end{aligned}$$

$(\Leftarrow)$ Suppose $\varphi(1)=\varphi(2)=0$. Then, it is clear from [Equation 1.12](#) that

+   a. $E[\cos\mathcal{Y}]=E[\sin\mathcal{Y}]=0$
+    b. $E[\cos 2\mathcal{Y}]=E[\sin 2\mathcal{Y}]=0$

From [Equation 1.13](#), we see that (a) implies $E[X(t)]=0$. Also, upon taking the expectation of $X(t)X(t+h)$ in [Equation 1.14](#), it is seen that (b) implies

$$\gamma(h)=E[X(t)X(t+h)]=\frac{C^2}{2}\cos(\lambda h),$$