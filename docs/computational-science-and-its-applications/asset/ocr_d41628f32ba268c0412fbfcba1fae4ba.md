![](bbox=[0.21, 0.115, 0.79, 0.415])

**FIGURE 7.1**  
Conformable fractional heat equation for α = 0.5.

Substituting Equation (7.15) in Equation (7.14), we obtain the solution

$$u(x,t)=\sum_{n=1}^{\infty}\sin\left(\frac{n\pi x}{L}\right)e^{-\left(\frac{n\pi}{L}\right)^2\frac{k t^{\alpha}}{\alpha}}\left[\frac{2}{L}\int_{0}^{L}f(x)\sin\left(\frac{n\pi x}{L}\right)dx\right].$$

The MATLAB® simulation of the fractional heat equation is given in Figure 7.1.

```
```matlab
[X, T] = meshgrid (0: 0.1: 2,1: 21);
alpha=0.5;
k=0.1;
L=2;
f(x)=sin(x);
u=0;
for n=1:20
fun=@(X) (sin(X).*sin((n.*pi.*X)./(L)));
format long
q=integral(fun,0,L);
u=u+sin((n.*pi.*X)./(L)).*exp(-(((n.*pi)./(L)).^2).*(k./alpha).*T.^
(alpha)).*(2./L).*q;
end
surf(T,X,u)
```
```

# 7.4 Simulation of Conformable Fractional Derivative of  
Harmonic Oscillator

The fractional harmonic oscillator is model [30] by