# 12.6.3 Shape from Surface Normals

Suppose we have the two partial derivatives, \(\frac{\partial z}{\partial x}\) and \(\frac{\partial z}{\partial y}\); we have the derivative of \(z\) and we want \(z\) – some calculus professor somewhere said we should integrate. Let’s try to do that. Since the objective of this book is to illustrate simple principles and not go into sophisticated math any more than necessary, we present a simple strategy here. No, it’s not the best, but it should illustrate the principles.

+   1. Start with x = 0 and y = 0
+   2. Set pixel (x, y) to zero.
+   3. Range over values of y
+      (a) range over values of x
+          • set z(x, y) <- z(x - 1, y) + p(x - 1, y).
+      (b) increment y and set x to zero.
+      (c) set z(x, y) <- z(x, y - 1) + q(x, y - 1)

Observe that the algorithm above is going through the image in a raster scanning way, incrementing z by p at every point first, and then doing one increment by q per line. There are other ways to walk through the image, other paths to take. If it should turn out that we get the same image z no matter which path we take, we say that this is an integrable function. In order to be integrable, a function should be continuous and differentiable.

Many papers and Horn’s classic text [12.18] address approaches for solving various special cases of the shape from shading problem. A paper by Zhang [12.61] surveys the field between Horn’s book and 1999. (Remember, Eq. 12.78 is itself a special case – it assumes the brightness does not depend on the observation angle). In the following, we discuss another special case, photometric stereo.

# 12.6.4 Photometric Stereo

In many cases, it is reasonable to model the reflectivity of a surface as proportional to the cosine of the angle between the surface normal vector and the illumination vector, a Lambertian reflectance model:

```
\(R(x, y) = r_a \mathbf{N}_i \cdot \mathbf{n}\) (12.80)
```

where \(\mathbf{N}_i\) is a unit vector\(^9\) in the direction of light source \(i\), and \(\mathbf{n}\) is the unit normal to the surface. If we are fortunate enough to have an object, a Lambertian reflector, that satisfies this equation, and which possesses the same albedo (\(r_a\)), independent of the illumination, we can make use of multiple pictures from multiple angles (not all sources in a single straight line) to determine the surface normal [12.19, 12.57]. Let us illuminate a particular pixel with three different light sources (one at a time) and measure the brightness of that pixel each time. At a given pixel, we construct a vector from the three observations

```
\(\mathbf{R} = [R_1, R_2, R_3]^T\) (12.81)
```

\(^9\) Huh? Earlier we said “cosine.” There’s no cosine in Eq. 12.80. How can this be explained?