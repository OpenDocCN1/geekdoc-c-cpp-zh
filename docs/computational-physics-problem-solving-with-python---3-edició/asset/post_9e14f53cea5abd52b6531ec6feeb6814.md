
in it. The hole contains a conducting disk of slightly smaller radius kept at potential V and separated from the sheet by a thin ring of insulating material. solves for the potential a perpendicular distance z above the edge of the disk in terms of an elliptic integral:

```
Φ(z) = V/2 ( 1 - (k z)/(π a) ∫₀^{π/2} dφ / √(1 - k² sin² φ) ) , (5.85)
```

where k = 2a / (z² + 4a²)^{1/2}. Use numerical integration to calculate and then plot the potential for V = 1, a = 1 and values of z in the interval (0.05, 10). Compare to a 1/r fall off.

6. Figure 5.7 shows a current loop of radius a carrying a current I. The point P is a distance r from the center of the loop with spherical coordinates (r, θ, φ). Jackson (1988) solves for the φ component of the vector potential at point P in terms of elliptic integrals:

```
A_φ(r, θ) = μ₀/(4π) * 4 I a / √(a² + r² + 2 a r sin θ) [ (2 - k²)K(k) - 2E(k) ] / k² , (5.86)
```

```
K(k) = ∫₀^{π/2} dφ / √(1 - k² sin² φ) ,   E(k) = ∫₀^{π/2} √(1 - k² sin² φ) dφ , (5.87)
```

```
k² = 4 a r sin θ / (a² + r² + 2 a r sin θ) . (5.88)
```

Here K(k) is a complete elliptic integral of the first kind and E(k) is a complete elliptic integral of the second kind. For a = 1, I = 3, and μ₀/4π = 1, compute and plot

+   a) A_φ(r = 1.1, θ) vs. θ.
+   b) A_φ(r, θ = π/3) vs. r.

## 5.17

## Multidimensional Monte Carlo Integration (Problem)

Let us say that we want to calculate some properties of a small atom such as magnesium with 12 electrons. To do that, we need to integrate atomic wave functions over the three coordinates of each of 12 electrons. This amounts to a 3 × 12 = 36D integral. If we use 64 points for each integration, this requires about 64³⁶ ≈ 10⁶⁵ evaluations of the integrand. If the computer were fast and could evaluate the integrand a million times per second, this would take about 10⁵⁹ s, which is significantly longer than the age of the universe (~ 10¹⁷ s).

![](img/bccda43674e4a93dee81c749eba8d2f7_132_0.png)

Figure 5.7 A ring of radius a carries a current I. Find vector potential at point P.

Your problem is to find a way to perform multidimensional integrations so that you are still alive to savor the results. Specifically, evaluate the 10D integral

```
I = ∫₀¹ dx₁ ∫₀¹ dx₂ ⋯ ∫₀¹ dx₁₀ (x₁ + x₂ + ⋯ + x₁₀)² . (5.89)
```

Check your numerical answer against the analytic one, 155/6.

It is easy to generalize mean value integration to many dimensions by picking random points in a multidimensional space. For example, in 2D:

```
∫ₐᵇ dx ∫ᶜᵈ dy f(x, y) ≈ (b−a)(d−c) 1/N Σᵢᴺ f(xᵢ) = (b−a)(d−c)⟨f⟩ . (5.90)
```

### 5.17.1

### Multi Dimension Integration Error Assessment

When we perform a multidimensional integration, the relative error in the Monte Carlo technique, being statistical, decreases as 1/√N. This is valid even if the N points are distributed over D dimensions. In contrast, when we use these same N points to perform a D-dimensional integration as D separate 1D integrals using a rule such as Simpson's, we use N/D points for each integration. For fixed N, this means that the number of points used for each integration decreases as the number of dimensions D increases, and so the error in each integration increases with D. Furthermore, the total error will be approximately N times the error in each integral. If you put these trends together and do the analysis for a particular integration rule, you will find that at a value of D ≈ 3−4 the error in Monte Carlo integration is approximately equal to that of conventional schemes. For larger values of D, the Monte Carlo method is always more accurate!

### 5.17.2

### Implementation: 10D Monte Carlo Integration

Use a built-in random-number generator to perform the 10D Monte Carlo integration in (5.89).

+   1. Conduct 16 trials and take the average as your answer.
+   2. Try sample sizes of N = 2, 4, 8, ..., 8192.
+   3. Plot the relative error vs. 1/√N and see if linear behavior occurs.
+   4. What is your estimate for the accuracy of the integration?
+   5. Show that for a dimension D ≈ 3–4, the error in multidimensional Monte Carlo integration is approximately equal to that of conventional schemes, and that for larger values of D, the Monte Carlo method is more accurate.

## 5.18

## Integrating Rapidly Varying Functions (Problem)

It is common in many physical applications to integrate a function with an approximately Gaussian dependence on x. The rapid falloff of the integrand means that our Monte Carlo integration technique would require an incredibly large number of points to have sufficient points where the integrand is large. Your problem is to make Monte Carlo integration more efficient for rapidly varying integrands.

## 5.19

## Variance Reduction (Method)

If the function being integrated never differs much from its average value, then the standard Monte Carlo mean value method (5.79) should work well with a large, but manageable, number of points. Yet for a function with a large variance (i.e., one that is not “flat”), many of the evaluations of the function may occur for x values at which the function is very small, and thus makes an insignificant contribution to the integral; this is, basically, a waste of time. The method can be improved by mapping the function f into a different function g that has a smaller variance over the interval. We indicate two methods here and refer you to Press et al. (1994) and Koonin (1986) for more details.

The first method is a variance reduction or subtraction technique in which we devise a flatter function on which to apply the Monte Carlo technique. Suppose we construct a function g(x) with the following properties on [a, b]:

```
|f(x) − g(x)| ≤ ε ,    ∫ₐᵇ dx g(x) = J .    (5.91)
```

We now evaluate the integral of the difference $f(x)-g(x)$ and add the result to $J$ to obtain the required integral

$$\int_a^b dx\,f(x)=\int_a^b dx\,[f(x)-g(x)]+J.$$  \tag{5.92}

If we are clever enough to find a simple $g(x)$ that makes the variance of $f(x)-g(x)$ less than that of $f(x)$, and that we can integrate analytically, we can obtain even more accurate answers in less time.

## 5.20  
**Importance Sampling (Method)**

A second method for improving Monte Carlo integration is called *importance sampling* because samples the integrand in the most important regions. It derives from the identity

$$I=\int_a^b dx\,f(x)=\int_a^b dx\,w(x)\frac{f(x)}{w(x)}.$$  \tag{5.93}

If we now use a *probability distribution* for our random numbers that includes $x(x)$, the integral can be approximated as

$$I=\left\langle\frac{f}{w}\right\rangle\simeq\frac{1}{N}\sum_{i=1}^{N}\frac{f(x_i)}{w(x_i)}.$$  \tag{5.94}

The improvement arising from (5.94) is that with a judicious choice of weighting function $w(x)\propto f(x)$, we can make $f(x)/w(x)$ more constant and thus easier to integrate accurately.

## 5.21  
**von Neumann Rejection (Method)**

A simple and ingenious method for generating random points with a probability distribution $w(x)$ was deduced by von Neumann and is implemented in Listing 5.3. This method is essentially the same as the rejection or sampling method used to guess the area of a pond, only now the pond has been replaced by the weighting function $w(x)$, and the arbitrary box around the lake by the arbitrary constant $W_0$. Imagine a graph of $w(x)$ vs. $x$ (Figure 5.8). Walk off your box by placing the line $W=W_0$ on the graph, with the only condition being $W_0\geq w(x)$. We next “throw stones” at this graph and count only those splashes that fall into the $w(x)$ pond. That is, we generate uniform distributions in $x$ and $y\equiv W$ with

```
incr = 2.0*pi/N
for i in range(0,N):
    xx = i*incr
    xsinx.x[i] = ((80.0/pi)*xx-80)
    xsinx.y[i] = 20.0*fx(xx)-50
    box = curve(pos=[(-80,-50), (-80,50), (80,50), (80,-50), (-80,-50)], color=color.white)      # box

plotfunc()                                                                 # Box area = h x w =5*2pi
j = 0
Npts = 3001                                                                 # Pts inside box
analyt = (pi)* *2                                                          # Analytical integral
areanal.text = 'analytical=%8.5f '%analyt
genpts = points(size=2)
for i in range(1,Npts):                                                     # points inside box
    rate(500)                                                               # slow process
    x = 2.0*pi*random.random()
    y = 5*random.random()
    xp = x*80.0/pi-80
    yp = 20.0*y-50
    pts2.text = '%4s ' %i
    if y <= fx(x):
        j += 1
        genpts.append(pos=(xp,yp), color=color.cyan)
        inside2.text='%4s %'
    else: genpts.append(pos=(xp,yp), color=color.green)
boxarea = 2.0*pi*5.0
area = boxarea*j/(Npts-1)
arealb2.text = '%8.5f '%area
```

### 5.21.1

### Simple Random Gaussian Distribution

The central limit theorem can be used to deduce a Gaussian distribution via a simple summation. The theorem states, under rather general conditions, that if {r_i} is a sequence of mutually independent random numbers, then the sum

x_N = Σ_{i=1}^N r_i  (5.97)

is distributed normally. This means that the generated x values have the distribution

P_N(x) = exp[ - (x-μ)^2 / (2σ^2) ] / sqrt(2πσ^2) ,   μ = N⟨r⟩ ,   σ^2 = N(⟨r^2⟩ - ⟨r⟩^2).   (5.98)

## 5.22

## Nonuniform Assessment ⊙

Use the von Neumann rejection technique to generate a normal distribution of standard deviation 1 and compare it to the simple Gaussian method.
