are:

In this

```
$$\omega_f = 2\pi f_f$,$
T = 1/f_f$,$
$\alpha_p = \tan\left(\frac{\omega_f T}{2}\right)$,$
g = \frac{\omega_f T}{2} \quad R = \frac{1}{2Q}$,$
$\alpha_s = \frac{1}{1+2Rg+g^2} \quad \alpha_c = \alpha_g = g$
```

implementation, you first calculate $y_{HP}(n)$:

and use it to feed the

rest of the structure. Method of finding that the inner loop is one of which you can derive the implementation of these VA filters, although you can approach it differently and calculate other outputs or inputs to the sections. For any given structure, there are several different implementation approaches, all of which produce the same result. We prefer to use the approach that yields the simplest block diagram with the least number of coefficients and equations.

The bandpass and lowpass outputs are:

We can also

```
$y_{BP}(n) = \alpha_b y_{in}(n) + s_b(n)$,$
y_{LP}(n) = \alpha_l y_{in}(n) + s_l(n)$
```

generate the missing bandstop filter output by using another shortcut:

```
$y_{BS}(n) = x(n) - 2Ry_{in}(n)$
```

Each output of this

filter produces another VA filter with the instantaneous response equation $y = Gx + S$. For the highpass $y_{HP}$, we can expand the equation out to see this.

The

```
$y_{out}(n) = \alpha_s(x(n) - \rho_s(n) + s_s(n))$,$
x - \(2R+g)s_1 - s_2$,$
\frac{1}{1+2Rg+g^2}$,$
= Gx + S$,$
where
G = \frac{1}{1+2Rg+g^2}$,$
S = \frac{-(2R+g)s_1 + s_2}{1+2Rg+g^2}$
```

derivations for the LP and BP outputs are left as an exercise for the reader. The answers are:

```
$y_{LP} = Gx + S$,$
G = \frac{1}{1+2Rg+g^2}$,$
S = \frac{-(2R+g)s_1 + g_1 + s_2}{1+2Rg+g^2}$,$
y_{BP} = Gx + S$,$
G = \frac{1}{1+2Rg+g^2}$,$
S = \frac{g_2 - g_1 + s_2}{1+2Rg+g^2}$
```