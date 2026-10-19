# 5.6

# Second Derivatives (Problem)

Let us say that you have measured the position $y(t)$ vs. time for a particle (Figure 5.1). Your *problem* now is to determine the force on the particle. Newton's second law tells us that force and acceleration are linearly related:

```
$$F = ma = m \frac{\mathrm{d}^2 y}{\mathrm{d} t^2}, \tag{5.20}$$
```

where $F$ is the force, $m$ is the particle's mass, and $a$ is the acceleration. So by determining the derivative $\mathrm{d}^2 y/\mathrm{d} t^2$ from the $y(t)$ values, we determine the force.

The concerns we expressed about errors in first derivatives are even more valid for second derivatives where additional subtractions may lead to additional cancelations. Let us look again at the central-difference method:

```
$$\left.\frac{\mathrm{d}y(t)}{\mathrm{d}t}\right|_{\mathrm{cd}} \simeq \frac{y(t+h/2)-y(t-h/2)}{h}. \tag{5.21}$$
```

This algorithm gives the derivative at $t$ by moving forward and backward from $t$ by $h/2$. We take the second derivative $\mathrm{d}^2 y/\mathrm{d} t^2$ to be the central difference of the first derivative:

```
$$\left.\frac{\mathrm{d}^2 y(t)}{\mathrm{d} t^2}\right|_{\mathrm{cd}} \simeq \frac{y'(t+h/2)-y'(t-h/2)}{h}$$
```

```
$$\simeq \frac{[y(t+h)-y(t)]-[y(t)-y(t-h)]}{h^2} \tag{5.22}$$
```

```
$$= \frac{y(t+h)+y(t-h)-2y(t)}{h^2}. \tag{5.23}$$
```

As we did for the first derivatives, we determine the second derivative at $t$ by evaluating the function in the region surrounding $t$. Although the form (5.23) is more compact and requires fewer steps than (5.22), it may increase subtractive cancellation by first storing the "large" number $y(t+h)+y(t-h)$ and then subtracting another large number $2y(t)$ from it. We ask you to explore this difference as an exercise.

# 5.6.1

# Second-Derivative Assessment

Write a program to calculate the second derivative of $\cos t$ using the central-difference algorithms (5.22) and (5.23). Test it over four cycles. Start with $h \simeq \pi/10$ and keep reducing $h$ until you reach machine precision. Is there any noticeable differences between (5.22) and (5.23)?