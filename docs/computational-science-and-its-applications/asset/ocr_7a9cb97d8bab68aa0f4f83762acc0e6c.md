# 7.6  Simulation of Conformable Fractional Derivative of Sine-Cosine Wavelet

Sine-cosine wavelets $\psi_{n,m}(t)=\psi(k,n,m,t)$ involve four arguments, $k=0,1,2,\ldots,n=0,\ldots,2^k-1$, the values $m$ are given in Equation (7.19) and $t$ is the normalized time. They are defined on the interval $[0,1]$ as [41, 47, 54, 61]

$$\psi_{n,m}(t)=\begin{cases}2^{\frac{k+1}{2}}f_m(2^kt-n),&\frac{n}{2^k}\le t\le\frac{n+1}{2^k}\\0,&\text{otherwise.}\end{cases} \tag{7.18}$$

where

$$f_m(t)=\begin{cases}\frac{1}{\sqrt{2}},&m=0\\\cos(2m\pi t),&m=1,2,\ldots,L\\\sin 2(m-L)\pi t,&m=L+1,L+2,\ldots,2L.\end{cases} \tag{7.19}$$

We used Equation (7.3) for the conformable fractional derivative

$$\frac{d^\alpha f_m}{dt^\alpha}=t^{1-\alpha}f'_m(t),$$

where

$$f'_m(t)=\begin{cases}0,&m=0\\-2m\pi\sin 2m\pi t,&m=1,2,\ldots,L\\2(m-L)\pi\cos 2(m-L)\pi t,&m=L+1,L+2,\ldots,2L.\end{cases}$$

MATLAB program for conformable fractional derivative of sine wavelet:

```
t=linspace(0,1,20);
L=20;
[T, m]=meshgrid (t, 1: L);
alpha=0.5;
Y=(T.^(1-alpha)).* (cos(2.*(m - L).*pi.*T)) .*(2.*(m - L).*pi);
surf(T,m,Y)
MATLAB program for conformable fractional derivative of cosine wavelet:
t=linspace(0,1,20);
L=20;
[T, m]=meshgrid (t, 1: L);
alpha=0.5;
Y=(T.^(1-alpha)).*(-sin(2.*m.*pi.*T)).*2.*m.*pi;
surf(T,m,Y)
```

Figure 7.5 represents the conformable fractional derivative of sine–cosine wavelet.