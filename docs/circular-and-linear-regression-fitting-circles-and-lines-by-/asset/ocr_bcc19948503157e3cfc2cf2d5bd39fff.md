can rarely afford slow iterative geometric fits, hence a noniterative algebraic fit may very well be the only option.

Last but not the least, well designed algebraic fits (such as Taubin's and Pratt's algorithms described in this chapter) appear to be nearly as accurate, statistically, as geometric fits (this will be confirmed by our detailed error analysis in Chapter 7). In many applications a good algebraic fit would do an ex- cellent job, and subsequent geometric fits would not make noticeable improve- ments.

# 5.1 Simple algebraic fit (Kåsa method)

Perhapes the simplest and most obvious approach to the circle fitting problem is to minimize

```
$$\mathscr{F}_1(a, b, R) = \sum_{i=1}^{n} \left[ (x_i - a)^2 + (y_i - b)^2 - R^2 \right]^2. \quad \quad \quad \quad (5.1)$$
```

In other words, we are minimizing $\mathscr{F}_1 = \sum f_i^2$, where

```
$$f_i = (x_i - a)^2 + (y_i - b)^2 - R^2. \quad \quad \quad \quad (5.2)$$
```

Clearly, $f_i = 0$ if and only if the point $(x_i, y_i)$ lies on the circle; also, $f_i$ is small if and only if the point lies near the circle. Thus, minimizing (5.1) sounds like a reasonable idea. Some authors [62, 67, 150] call $f_i$ the *algebraic distance* from the point $(x_i, y_i)$ to the circle $(x - a)^2 + (y - b)^2 + R^2 = 0$.

The derivatives of the objective function (5.1) are nonlinear with respect to $a, b, R$, but a simple change of parameters makes them linear. Let

```
$$B = -2a, \quad \quad C = -2b, \quad \quad D = a^2 + b^2 - R^2. \quad \quad \quad \quad (5.3)$$
```

Then we get

```
$$\mathscr{F}_1 = \sum_{i=1}^{n} (z_i + Bx_i + Cy_i + D)^2 \quad \quad \quad \quad (5.4)$$
```

where we also denote $z_i = x_i^2 + y_i^2$ for brevity.

Now differentiating $\mathscr{F}_1$ with respect to $B, C, D$ yields a system of *linear* equations

```
$$\begin{array}{rrcl} \overline{x x}B + \overline{x y}C + \overline{x}D &=& -\overline{x z} \\ \overline{x y}B + \overline{y y}C + \overline{y}D &=& -\overline{y z} \\ \overline{x}B + \overline{y}C + D &=& -\overline{z}, \end{array} \quad \quad \quad \quad (5.5)$$
```

where we again use our “sample mean” notation

```
$$\overline{x x} = \frac{1}{n} \sum x_i^2, \quad \quad \overline{x y} = \frac{1}{n} \sum x_i y_i, \quad \text{etc.}$$
```