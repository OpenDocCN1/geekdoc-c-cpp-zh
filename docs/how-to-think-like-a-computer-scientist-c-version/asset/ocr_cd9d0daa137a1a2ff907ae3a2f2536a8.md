# Cartesian coordinates

# Polar coordinates

imaginary axis

![](bbox=[0.231, 0.305, 0.833, 0.381])

magnitude

angle

real axis

Complex numbers in polar coordinates are written $re^{\theta}$, where $r$ is the magnitude(radius), and $	heta$ is the angle in the radians.
Fortunately, it is easy to convert from one form to another. To go Cartesian to polar,

$r = \sqrt{x^2 + y^2}$
$\theta = \arctan(y/x)$

To go from polar to Cartesian,

$x = r\cos\theta$
$y = r\sin\theta$

So which representation should we use? Well, the whole reason there are multiple representations is that some operations are easier to perform in Cartesian coordinates (like addition), and others are easier in polar coordinates (like multiplication). One option is that we can write a class definition that both representations, and that converts between them automatically, as needed.

```
class Complex
{
    double real, imag;
    double mag, theta;
    bool cartesian, polar;

public:
    Complex () { cartesian = false; polar = false; }

Complex(double r, double i)
```