![](bbox=[0.42, 0.11, 0.58, 0.2])

Figure 3.4 The main idea behind Gordon-Wixom interpolation consists of combining linear interpolation for each chord passing through x with circular averaging with respect to all directions eg.

potentially good substitutes for harmonic coordinates [215]. Below we consider a pseudo-harmonic transfinite barycentric interpolation scheme introduced initially by Gordon and Wixom [171] and then studied and extended by a number of researchers [37, 38, 145, 146, 266].

Following [171], let us call a transfinite barycentric interpolation scheme pseudo-harmonic if it reproduces harmonic functions in a ball (a disk in the 2D case). It turns out that transfinite mean value (3.4), Laplace (3.13), and Wachspress coordinates (3.16) are not pseudo-harmonic. In contrast, the Gordon-Wixom interpolation scheme [171] and some of its generalizations and modifications [37, 38] are pseudo-harmonic.

The basic idea behind the approach of Gordon and Wixom is simple and elegant. Given a point x inside a bounded convex domain Omega subset R^2, consider a straight line passing through x, forming an angle theta with some fixed direction, and intersecting partial Omega in two points y1 and y2 (see Figure 3.4). We then use linear interpolation between u(y1) and u(y2) to obtain an estimate u(x, theta) associated with the direction theta,

```
[(u(y1) + u(y2)) / rho1] / [1/rho1 + 1/rho2]
```

Circular averaging of u(x, theta) with respect to theta then yields the Gordon-Wixom interpolation of some function u from partial Omega to x in Omega,

```
u(x) = 1/(2pi) int_0^{2pi} [ (u(y1)/rho1 + u(y2)/rho2) / [1/rho1 + 1/rho2] ] dtheta. (3.18)
```

To demonstrate that the Gordon-Wixom interpolation scheme is pseudo-harmonic, we rewrite (3.18) as

```
u(x) = 1/pi int_0^{2pi} (rho2 / (rho1 + rho2)) u(y1) dtheta (3.19)
```

and assume that Omega is a disk of radius R. We now recall that, according to the intersecting chords theorem,

```
rho1 rho2 = c(x),
```

where c(x) depends only on x. In the notation of Figure 3.5 we further have

```
h1 = rho1 sin phi, h2 = rho2 sin phi, rho1 + rho2 = 2R sin phi,
```