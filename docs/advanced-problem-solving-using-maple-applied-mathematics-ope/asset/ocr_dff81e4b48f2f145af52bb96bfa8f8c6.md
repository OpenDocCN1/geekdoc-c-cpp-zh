data points via cubic polynomials to form a piecewise curve. These curves are called “cubic splines,” cubic for the third degree and spline after the flexible draftsman’s ruler originally used to draw the curves. The data points are called “knots.” Pierre Bézier, a French design engineer at Renault, introduced using splines for designing auto bodies in the 1960s. Splines are ubiquitous today, appearing in numerous applications. TrueType, developed by Apple in the 1990s, uses two-dimensional quadratic splines to form the characters on your phone or computer screen, and PostScript, developed by Adobe in the 1980s, uses two-dimensional cubic splines for printed characters.

# Example 5.6. Natural Cubic Splines as a System of Equations.

Fit a natural cubic spline⁷ to the data

| $x$ | 7 | 14 | 21 | 28 | 35 | 42 |
|---|---:|---:|---:|---:|---:|---:|
| $y$ | 125 | 275 | 800 | 1200 | 1700 | 1650 |

We will need 5 third order equations.

for $x \in [7,14]$: $S_1(x)=a_{1,3}x^3+a_{1,2}x^2+a_{1,1}x+a_{1,0}$

for $x \in [14,21]$: $S_2(x)=a_{2,3}x^3+a_{2,2}x^2+a_{2,1}x+a_{2,0}$

for $x \in [21,28]$: $S_3(x)=a_{3,3}x^3+a_{3,2}x^2+a_{3,1}x+a_{3,0}$

for $x \in [28,35]$: $S_4(x)=a_{4,3}x^3+a_{4,2}x^2+a_{4,1}x+a_{4,0}$

for $x \in [35,42]$: $S_5(x)=a_{5,3}x^3+a_{5,2}x^2+a_{5,1}x+a_{5,0}$

There are 20 unknowns: $a_{i,j}$, so we need 20 equations to uniquely solve for these unknowns. The $(x,y)$ data pairs give 10 equations, $S_1(7)=125$, $S_1(14)=275$, $S_2(14)=275$, $S_2(21)=800$, and so forth. We need 10 more equations.

To make the spline smooth, we require the curve to have both first and second derivatives equal, i.e., match slope and concavity, at the knots (data points). So, for $i=1..4$, make

$S_i'(x_{i+1})=S_{i+1}'(x_{i+1})$ and $S_i''(x_{i+1})=S_{i+1}''(x_{i+1})$.

These requirements give us 8 more equations. For the last two equations, use the condition for “natural” splines:

$S_1'(x_1)=0$ and $S_5'(x_6)=0$

We have the requisite 20 equations. Let’s use Maple to build the equations, the augmented coefficient matrix, and find the spline.

> ⁷Natural cubic splines mimic the original engineer’s flexible ruler by requiring that the second derivative of the spline at the two end data points be 0. “Clamped” cubic splines use specified values for the first derivative at the two end data points.