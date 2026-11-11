
In this case, assigning half the probability to each successive path length makes some sense. In general, picking the right sampling distribution is at the heart of making such Monte Carlo approaches work well.

### 31.5.1.3 Solving $50x^{2.1}=13$ Stochastically

Applying these methods to our particular equation, we know that

$$x=\left(\frac{13}{50}\right)^{\frac{1}{2.1}}, \tag{31.19}$$

and that in general we can transform the right-hand side of the equation using the binomial theorem

$$(1+t)^\alpha=\sum_{k=0}^{\infty}\binom{\alpha}{k}t^k. \tag{31.20}$$

Doing so, with $t=\frac{13}{50}-1=-\frac{37}{50}$ and $\alpha=\frac{1}{2.1}$, we get

$$x=\left(\frac{13}{50}\right)^{\frac{1}{2.1}} \tag{31.21}$$
$$=\binom{\alpha}{0}+\binom{\alpha}{1}\left(-\frac{37}{50}\right)^1+\binom{\alpha}{2}\left(-\frac{37}{50}\right)^2+\cdots \tag{31.22}$$
$$=1+\frac{\alpha}{1}\left(-\frac{37}{50}\right)^1+\frac{\alpha(\alpha-1)}{2!}\left(-\frac{37}{50}\right)^2+\cdots. \tag{31.23}$$

Now, to estimate a solution, we pick a positive integer $j$ with probability $2^{-j}$, and evaluate the $j$th term. As we wrote this chapter, we flipped coins and counted the number of flips until heads, generating the sequence 3, 3, 1; our three estimates of $x$ are thus the third, third, and first terms of the series, multiplied by 8, 8, and 2, respectively:

$$x_1=8\frac{\alpha(\alpha-1)}{2!}\left(-\frac{37}{50}\right)^2\approx -0.5464, \tag{31.24}$$
$$x_2=x_1=-0.5464\ldots \tag{31.25}$$
$$x_3=2. \tag{31.26}$$

![](img/f464cd0043eb5336aa0543fe20a0561b_880_0.png)

Recall that the correct solution to the problem is 0.5265. The average of our three samples is $x=.3024$, which admittedly is not a very good estimate of the solution. When we used 10,000 terms, the estimate was 0.5217, which is considerably closer (see Figure 31.4).

You may be concerned that we’ve assumed we can write a power series for $x$, but that when we get to the rendering equation, such a rewrite may not be so easy. Fortunately, in the case of the rendering equation, the rewrite as an infinite series is actually quite easy, although estimating the sum of the resultant series still involves the same randomized approaches.

*Figure 31.4: A histogram of 500 estimates of the root of $50x^{2.1}=13$, their average is quite near 0.5265.*

## 31.6 Method 4: Bisection

Our final approach to solving the equation is to find a value of $x$ for which $50x^{2.1}$ is less than 13 (such as $x=0$) and one for which it’s greater than 13 (such as $x=1$).

Since \(f(x) = 50x^{2.1}\) is a continuous function of \(x\), it must take on the value 13 somewhere between \(x = 0\) and \(x = 1\). We can evaluate \(f(\frac{1}{2})\) and find that it’s less than 13; we now know that the solution’s between \(\frac{1}{2}\) and 1. Repeatedly evaluating \(f\) at the midpoint of an interval that we know contains the answer, and then discarding half the interval on the basis of the result, rapidly converges on a very small interval that must contain the solution.

This can be seen as a kind of binary search on the real line. There are also “higher order” methods, like Newton’s method, in which we start at some proposed solution \(x_0\) and say, “If \(f\) were linear, then we could write it as \(y = f(x_0) + f'(x_0)(x - x_0)\).” But that function is zero at \(x_1 = x_0 - \frac{f(x_0)}{f'(x_0)}\). So let’s evaluate \(f\) at \(x_1\) and see whether it’s any smaller there, and iterate. If \(x_0\) happens to be near a root of \(f\), this tends to converge to a root quite fast. If it’s not (or if \(f'(x_0) = 0\)), then it doesn’t work so well.

Despite the appeal of these approaches, there’s no easy analog in the case of functional equations (ones where the answer is a *function* rather than a number) like the rendering equation. There’s no simple way to generalize the notion of one number being between two others to the more general category of functions.

Nonetheless, bisection gets used a lot in graphics, and these four approaches to solving equations serve as archetypes for solving equations throughout the field.

## 31.7 Other Approaches

There are other approaches to equations that cannot be easily illustrated with our \(50x^{2.1} = 13\) example. For instance, you might say, “I can solve systems of two linear equations in two unknowns . . . but only if the coefficients are integers rather than arbitrary real numbers.” In doing so, you’re not really solving the general problem (“two linear equations in two unknowns”), but it may be that the subclass of problems you *can* solve is interesting enough to merit attention. In graphics, for instance, early rendering algorithms could only work with a few point lights rather than arbitrary illumination; some later algorithms could only work on scenes where all surfaces were Lambertian reflectors, etc.

As a second example, you may arrive at a method of solution that’s too complex, and choose to approximate the *method* of solution rather than the original equation. For instance, the Monte Carlo approach used to sum an infinite series above might seem overly complicated, and you might choose to just sum the first four terms. This *sounds* laughable, but in practice it can often work quite well. Most basic ray tracers, for instance, trace secondary rays only to a predetermined depth, which amounts to truncating a series solution after a fixed number of terms.

## 31.8 The Rendering Equation, Revisited

Recall that a radiance field is a function on the set \(\mathcal{M}\) of all surface points in our scene, and that it takes a point, \(P \in \mathcal{M}\), and a direction, \(\omega\), and returns a real number indicating the radiance along a ray leaving \(P\) in direction \(\omega\). Our model of the radiance field is a function \(L : \mathcal{M} \times S^2 \to \mathbb{R}\).

There is a subtlety here that we discussed in Section 29.4: There are some “surface points” that are part of two surfaces. For instance, if we have a solid glass sphere (see Figure 31.5), the point at the north pole of the sphere is really best thought of as *two* points: one on the “outside” and the other on the “inside.” Light traveling northward at the outer point is either reflected or transmitted, while light traveling northward at the inner point is *arriving* there and is about to be transmitted or reflected by the glass-air interface. As we suggested, we can enhance the notion of the light field to take three arguments—a point, a direction, and a normal vector that defines the “outside” for this point—but in the remainder of this chapter, we’re going to instead discuss *only* reflection (except at a few carefully indicated points), since (a) the two-points-in-one-place idea complicates the notation, which is complex enough already, and (b) the actual changes in the programs that we’ll see in Chapter 32 to account for transmission are relatively minor and straightforward. As for the matter of keeping two separate copies of the north pole, in practice, as we’ll discuss in Chapter 32, we’ll only keep a single copy of the geometry, and there will be no explicit representation of the light field; on the other hand, the meaning of an arriving light ray, and how it is treated, will depend on the dot product of its direction with the unit normal **n**, resulting in several `if-else` clauses in our programs.

![](img/f464cd0043eb5336aa0543fe20a0561b_882_0.png)

*Figure 31.5:* Light from above the sphere both reflects and refracts, as does light in the inside of the sphere.

We’ll continue to write f<sub>s</sub> for the scattering function, however, but you’ll need to remember that in the case of transmission, some ω · **n** terms may need absolute-value signs on them.

> **Notation:** In some papers, L<sub>on</sub> is L(P, ω) and L<sub>out</sub> is L(P, −ω). Jensen uses L<sub>f</sub> for reflected radiance, L<sub>i</sub> for incoming radiance, and L<sub>t</sub> for transmitted radiance. RTR does the same thing. RTR uses L<sub>s</sub> and L<sub>e</sub>, with the direction changing based on the subscript. Shirley uses k<sub>i</sub> and k<sub>o</sub> for ω<sub>i</sub> and ω<sub>o</sub>; Arvo calls L<sub>i</sub> and L<sub>o</sub> “field” and “surface” radiance. By the way, what we call the radiance field is also called the “plenoptic function” and the “light field.”

The rendering equation characterizes the radiance field (P, ω) → L(P, ω) in a scene by saying that the radiance at some surface point, in some direction, is a sum of (a) the radiance *emitted* at that point in that direction, and (b) all the incoming light at that point that is scattered in that direction. This equation has the form

$$L = E + T(L). \tag{31.27}$$

Recall the meaning of the terms:

- *E* is the *emitted* radiance field, with E(P, ω) = 0 unless P is a point of some luminaire, and ω is a direction in which that luminaire emits light from P.
- *T(L)* is the scattered radiance field due to L; T(L)(P, ω<sub>o</sub>) is the light scattered from the point P in the direction ω<sub>o</sub> when the radiance field for the whole scene is L.<sup>1</sup>

To be specific, T is defined by

$$T(L)(P, \omega_o) = \int_{\omega_i \in S^2} L(P, -\omega_i) f_s(P, \omega_i, \omega_o) (\omega_i \cdot n(P)) \, d\omega_i. \tag{31.28}$$

1\. We use the letter T rather than S (for “scattering”) because S will be used later in describing various light paths.
