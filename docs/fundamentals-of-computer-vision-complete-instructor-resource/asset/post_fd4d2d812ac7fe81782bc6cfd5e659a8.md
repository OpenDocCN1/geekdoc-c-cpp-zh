
![](img/5f95dd954ac63cc68119f6f48ca99e18_347_0.png)

Figure 12.15 Light strikes a surface at an incident angle, relative to the surface normal, N, and is reflected/scattered in another direction.

Despite the fact that we use the term “brightness” constantly, it actually does not have a rigorous physical definition. Horn [12.18] reminds us that we should define irradiance as the power per unit area falling on a surface, measured in watts per square meter. Then, radiance is defined as the power per unit foreshortened area per unit solid angle. This dependence on foreshortened area makes it clear that both the angle of observation and the angle of incidence may play important roles in scene “brightness.”

At a point, the reflectivity model of a surface relates the surface normal, the direction to the light source, and the direction of the observer. For example, the reflected brightness might be related to the incident brightness with a relationship such as

$$R(x, y) = r_0 f(x, y) \cos(\theta_i).$$ (12.75)

Thus, if we know the incident brightness f, the albedo (how the surface is painted) r0, and the reflected brightness R, we might hope to solve for θi, and from that, infer the surface normal, and from that the surface. The reflectivity function of Eq. 12.75 is known as a Lambertian model. Note that the angle of observation does not enter the Lambertian model. Try this: look at a white styrofoam cup and you will see that no matter how you turn it in front of your eyes, the brightness does not change, so the apparent reflected light is independent of the angle of observation. However, put it close to a single light source and you will see that the angle of incidence does matter in how bright the surface appears. Another familiar reflectivity function is the specular model

$$R(x, y) = r_0 f(x, y) \delta(\theta_i - \theta_o),$$ (12.76)

which describes mirrors – you only get a reflection if the angle of illumination equals the angle of incidence. Of course most surfaces, even “shiny” ones, are not perfect specular reflectors, and a more realistic model for a mixed surface might be

$$R(x, y) = r_0 f(x, y) \cos^4(\theta_i - \theta_o).$$ (12.77)

Although the use of reflectivity functions requires radiometric calibration of cameras [12.16], that requirement in itself is not the major difficulty. To see the complexity of the problem [12.33] let us expand Eq. 12.75 in terms of the elements of the unit incidence vector I = [I_x, I_y, I_z]^T and the normal vector, n, recalling that the inner product of these two vectors will be cos θ.

```
\( R(x, y) = r_0 f(x, y) \mathbf{I} \cdot \mathbf{n} = r_0 f(x, y) \left( I_x \frac{\partial z}{\partial x} + I_y \frac{\partial z}{\partial y} + I_z \right). \quad (12.78) \)
```

Assuming we know the angle of incidence θ (which we will actually know only approximately), the albedo r0, and the incident brightness f, we will still have a partial differential equation that we must solve to determine the surface function z.

So how do we do that – solve this ugly partial differential equation? We can do it if we have p and q, but that is a challenging problem in itself. There are a variety of approaches, (See the text by Horn [12.18]) the details of which are beyond the scope of this book. Basically, a numeric differential equation solver is used to estimate z(x, y) taking into account the boundary conditions of the object being estimated, as well as agreeing with the local gradient information provided by shading.

## 12.6.2 Using Shape from Shading with Two Light Sources

Here we will illustrate how to use shape-from-shading when two light sources are available. We will not go into the physics here, but scanning electron microscopes provide an excellent application. In such a microscope two images are produced, one from secondary emission (SE) electrons and one from backscattered (BSE) electrons.

![](img/5f95dd954ac63cc68119f6f48ca99e18_348_0.png)

Figure 12.16 A given measured brightness pair can be created by a locus of p, q values in both SE and BSE images. (The authors are grateful to B. Karakci for this figure.)

Rather than attempting to model the geometry of the camera(s) exactly, we may simply measure the reflectivity functions RSE and RBSE by placing a sphere in the microscope and imaging it. On a sphere, p and q are easy to determine. For example, a particular brightness value might be represented by the locus of points shown in Figure 12.16. Then,

![](img/5f95dd954ac63cc68119f6f48ca99e18_349_0.png)

Figure 12.17 An integrated circuit with 4 pads is illustrated on the left from the backscattered electron sensor. Combining with the secondary emission sensor and using the techniques of this section allows a range image to be produced, which is illustrated on the right. With this information, the heights of the pads and the defect can be easily determined. (The authors are grateful to B. Karaca for this figure.)

assuming the albedo is known (that is an important assumption), the measured brightness is a function of p and q in both the BSE and SE images. Although there is an infinite number of possible p, q values in each image, there are only two possible (p, q) pairs that can explain both the measured brightnesses. We thus solve for z(x, y) by defining an objective function and finding the surface that minimizes that function.

To accomplish this, first let \(\rho((p_1, q_1), (p_2, q_2))\) define a function that represents the difference in the surface normals defined by the two p, q ordered pairs. (it could, for example, be something as simple as the cosine of the angle between them. Then, we consider the difference between the surface normal defined by the \(i^{th} (p, q)\) pair and the vector that is normal to the surface at \(z(x, y)\), and write that difference as \(d(x,y) = \rho((\frac{\partial z}{\partial x}, \frac{\partial z}{\partial y}), (p, q))\). Finally, assuming that the two curves of Figure 12.16 intersect at m points (and making m a function of x, y to remind the reader that all this is being done for a single x, y point), we define an objective function as

```
E = \sum_{x,y} \left( \sum_i (d(x,y))^{-1} \right)^{-1} + \lambda \Lambda \qquad (12.79)
```

allowing \(\Lambda\) to be a regularization term such as piecewise linearity.

Use of this technique to inspect integrated circuits [12.21] is illustrated in Figure 12.17. A variation on the simple model given above occurs when the surface is not totally reflective. For example, at infrared wavelengths (and other wavelengths, to a lesser extent), the power measured coming from a surface is a combination of energy that is reflected and energy that is emitted (so called “black body radiation”) as a result of the temperature of the surface [12.29].

## 12.6.3 Shape from Surface Normals

Suppose we have the two partial derivatives, \(\frac{\partial z}{\partial x}\) and \(\frac{\partial z}{\partial y}\); we have the derivative of \(z\) and we want \(z\) – some calculus professor somewhere said we should integrate. Let’s try to do that. Since the objective of this book is to illustrate simple principles and not go into sophisticated math any more than necessary, we present a simple strategy here. No, it’s not the best, but it should illustrate the principles.

- 1. Start with x = 0 and y = 0
- 2. Set pixel (x, y) to zero.
- 3. Range over values of y
  - (a) range over values of x
    - set z(x, y) <- z(x - 1, y) + p(x - 1, y).
  - (b) increment y and set x to zero.
  - (c) set z(x, y) <- z(x, y - 1) + q(x, y - 1)

Observe that the algorithm above is going through the image in a raster scanning way, incrementing z by p at every point first, and then doing one increment by q per line. There are other ways to walk through the image, other paths to take. If it should turn out that we get the same image z no matter which path we take, we say that this is an integrable function. In order to be integrable, a function should be continuous and differentiable.

Many papers and Horn’s classic text [12.18] address approaches for solving various special cases of the shape from shading problem. A paper by Zhang [12.61] surveys the field between Horn’s book and 1999. (Remember, Eq. 12.78 is itself a special case – it assumes the brightness does not depend on the observation angle). In the following, we discuss another special case, photometric stereo.

## 12.6.4 Photometric Stereo

In many cases, it is reasonable to model the reflectivity of a surface as proportional to the cosine of the angle between the surface normal vector and the illumination vector, a Lambertian reflectance model:

```
\(R(x, y) = r_a \mathbf{N}_i \cdot \mathbf{n}\) (12.80)
```

where \(\mathbf{N}_i\) is a unit vector\(^9\) in the direction of light source \(i\), and \(\mathbf{n}\) is the unit normal to the surface. If we are fortunate enough to have an object, a Lambertian reflector, that satisfies this equation, and which possesses the same albedo (\(r_a\)), independent of the illumination, we can make use of multiple pictures from multiple angles (not all sources in a single straight line) to determine the surface normal [12.19, 12.57]. Let us illuminate a particular pixel with three different light sources (one at a time) and measure the brightness of that pixel each time. At a given pixel, we construct a vector from the three observations

```
\(\mathbf{R} = [R_1, R_2, R_3]^T\) (12.81)
```

\(^9\) Huh? Earlier we said “cosine.” There’s no cosine in Eq. 12.80. How can this be explained?
