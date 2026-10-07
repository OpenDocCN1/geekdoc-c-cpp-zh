# Non-Linear Differential Equations and Dynamical Systems

is the same that of the corresponding linear system; it is specified by the eigenvalues ($4.38a, b$) = (4.482a-d):

```
$0=\begin{matrix} a-\lambda & b \ c & d-\lambda \end{matrix}=(a-\lambda)(d-\lambda)-bc=\lambda^2-(a+d)\lambda+ad-bc=(\lambda-\lambda_-)(\lambda-\lambda_-),\n(4.482a-d)$
```

implying that the system is stable (unstable) if (4.483a) both eigenvalues (at least one eigenvalue) have (has) negative (positive) real parts [4.483b] [part 4.483c):

```
$2\lambda_{\pm}=a+d\pm(a-d)^2+bc)^{1/2}=\begin{cases}0<Re(\lambda_+)\ge Re(\lambda_-): & stable;\0<Re(\lambda_+)\ge Re(\lambda_-): & unstable.\end{cases}\n(4.483a-c)$
```

The theorem can be applied to a second-order system (4.484b) specified (problem 151) by a continuously differentiable function (4.484a):

```
$f(x,\dot{x},\ddot{x})\in c^1(|\mathbb{R}^3):\quad\ddot{x}=f(x,\dot{x},\ddot{x})=-ax+bx+O(x^2,\dot{x},\ddot{x}),\n(4.484a, b)$
```

this corresponds to the linear second-order system (2.81b) = (4.484b) = (4.484d):

```
$$\ddot{x}+2\lambda\dot{x}+\omega_0^2x=0:\quad a=\omega_0^2\begin{cases}>0 & attractor\<0 & repeller\end{cases},\\quad b=-2\lambda=\begin{cases}>0 & damping\>0 & amplification\end{cases},\n(4.484d-f)$
```

including combinations of attractor or repeller (4.484e) and damping or amplification (4.484f). The system is equivalent to the corresponding autonomous system (4.485a, b):

```
$v=\dot{x},\dot{v}=ax+by;\quad0=\begin{matrix}-\lambda & 1\a & b-\lambda\end{matrix}=\lambda^2-\lambda b+a=(\lambda-\lambda_+)(\lambda-\lambda_-),\n(4.485a-c)$
```

its eigenvalues (4.485c) are (4.486a):

```
$2\lambda_{\pm}=b\pm\sqrt{b^2-4a};\quad a<0:\quad\lambda_+>0>\lambda_-.\n(4.486a-c)$
```

In the case of a repeller (4.486b) one eigenvalue is positive (4.486c), leading to instability.