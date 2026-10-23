+   Count the number of vowels.

+   Remove all vowels.

+   Convert all characters to uppercase (without using toUpper).

+   Convert all characters to lowercase (without using toLower).

# 8.7.5 Projects

+   1. This project builds on top of project 4 (p.178). For this you will fill in an entire grid of values with intersection parameters for a set of geometry. Most images on computers are made as grids of values where the values give the colors. We do not quite have the ability to introduce colors and images yet, but we are getting close.
+   
+   For now you will fill an Array[Array[Double]] with the t parameters for a collection of geometry. You should write a function that takes the following arguments: location of the viewer as a 3-D point, forward direction for the viewer as a 3-D vector, up direction for the viewer as a 3-D vector, ${}^{4}$ a sequence of geometry (spheres or planes), and the number of cells across the square grid should be. You will cast one ray for each cell in the grid and see if it hits anything and if so, how far out it hits. Fill the grid with the values for a minimum intersection parameter.
+   
+   The grid represents a plane in space that is one unit in front of the viewer position with a top-left corner that is one unit up and one unit to the left. (You can find a left vector by doing the cross product of the up and forward vectors.) The grid extends to one unit to the right and one unit down. This is the basic approach for building images using ray tracing.

+   2. One of the useful things that you learn in calculus is that functions can be approximated. Your calculus text will mention both the MacLaurin series approximation and the Taylor series approximation. They are basically the same other than MacLaurn series are always taken about $x = 0$ and this is what we will be working with here. The definition of the MacLaurn series is
+   $$f(x) \sim \sum_{i} \frac{f^{(i)}(0)}{i !} x^{i}$$
+   
+   So this is the sum from $i=0$ up to some $n$ (or infinity if you want to be really accurate). In the sum we have $x$ raised to the $i$ power times the $i^{th}$ derivative of $f(x)$ evaluated at 0 divided by $i$ factorial. Obviously, this is a real pain to use on functions where taking the derivative is not easy. However, for some functions where the derivatives are straightforward, performing this approximation is very easy. Examples of that would be $e^{x}, \sin(x)$, and $\cos(x)$.
+   
+   Write a program that does a Maclaurin approximation of $\cos(x)$. That is not that hard because the derivative is $-\sin(x)$, which has a derivative of $-\cos(x)$ which goes to $\sin(x)$ then back to $\cos(x)$. Also note that you are always evaluating at $x=0$ so all the terms for sin go to zero.
+   
+   The first few terms in this series are:
+   $$1 - 0 - \frac{x^{2}}{2 !} + 0 + \frac{x^{4}}{4 !} - 0 - \frac{x^{6}}{6 !} + 0 + \frac{x^{8}}{8 !} + \ldots$$

> ${}^{4}$For a standard projection the up and forward directions should be perpendicular. However, the math works as long as they are not parallel. You simply get a distorted view in that case.