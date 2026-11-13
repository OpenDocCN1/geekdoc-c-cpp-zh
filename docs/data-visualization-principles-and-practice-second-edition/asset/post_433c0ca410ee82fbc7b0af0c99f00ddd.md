
Hence, to create the height plot shown in Figure 2.1, it is sufficient to issue a single `glColor3f` call before all the quads are drawn. The green color shown in the figure corresponds to the setting \( r = 0.3 \), \( g = 0.8 \), \( b = 0.37 \).

Besides specifying the object color, we must specify the light intensity and direction, i.e., the parameters \( I_l \) and \( \mathbf{L} \) in Equation (2.1). In OpenGL, lights are specified by a number of function calls. First, OpenGL must be set up to use the Phong lighting equation, by enabling the lighting mechanism. OpenGL supports several light sources (most implementations provide at least eight of them). The next step is to enable one of the light sources, say the first one. These two operations are accomplished by the function calls

```
glEnable(GL_LIGHTING);
glEnable(GL_LIGHT0);
```

After lighting and the desired light(s) are enabled, we can specify the light intensity model. As explained in the previous section, OpenGL uses a three-component light model, so the Phong lighting model (Equation (2.1)) is applied three times. Moreover, OpenGL allows us to separately specify the amount of light that interacts with the ambient, diffuse, and specular material components. Putting it all together, the lighting equations used by OpenGL are

\( I^R(p, \mathbf{v}, \mathbf{L}) = I^R_{amb}c^R_{amb} + I^R_{diff}c^R_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^R_{spec}c^R_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,,\)
\( I^G(p, \mathbf{v}, \mathbf{L}) = I^G_{amb}c^G_{amb} + I^G_{diff}c^G_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^G_{spec}c^G_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,,\) (2.3)
\( I^B(p, \mathbf{v}, \mathbf{L}) = I^B_{amb}c^B_{amb} + I^B_{diff}c^B_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^B_{spec}c^B_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,.\)

Here, the superscripts \( R \), \( G \), and \( B \) denote the color components. The triplet \( (I^R_{amb}, I^G_{amb}, I^B_{amb}) \) specifies the amount (intensity) of light that interacts with the ambient material component \( (c^R_{amb}, c^G_{amb}, c^B_{amb}) \), and is specified by the function call

```
glLightfv(GL_LIGHT0, GL_AMBIENT, I);
```

Here, \( I = (I^R_{amb}, I^G_{amb}, I^B_{amb}) \) is a vector of three floating-point values. The same function can be used to specify the diffuse and specular light intensities for all lights by replacing `GL_AMBIENT` with `GL_DIFFUSE` and `GL_SPECULAR`, respectively, and replacing `GL_LIGHT0` with the desired light name.

Finally, we must specify the direction and position of the light (see Section 2.2). This is achieved by the function call

```
glLightfv(GL_LIGHT0, GL_POSITION, p);
```

Here \(p = (p_x, p_y, p_z, p_w)\) is a vector of four floating-point values. If the fourth value \(p_w\) is zero, the light is directional with the direction \(\mathbf{L} = (p_x, p_y, p_z)\). If \(p_w\) is not zero, the light is point-like, its position being given by \((p_x/p_w, p_y/p_w, p_z/p_w)\).

However attractive, this rendering of the surface approximation has several limitations. Probably the most salient one is the “faceted” surface appearance, due to its approximation by flat-shaded quadrilaterals. This artifact is visible even when we use a relatively densely sampled dataset, such as the one in Figure 2.2. When using flat-shaded polygons, removing this visual artifact completely for a height plot of an arbitrary function implies rendering polygons with a size of one pixel. In our setup, this implies, in its turn, using a prohibitively high sampling density. Just to give an impression of the costs, on a screen of \(640 \times 480\) pixels, this strategy would require rendering over a hundred thousand polygons, and computing and storing a dataset of over a hundred thousand sample points, i.e., a memory consumption of a few hundred kilobytes, all for a simple visualization task.

### Smooth shading

We can easily improve on this by using _Gouraud shaded_, or smoothly shaded, quads. Gouraud shading assumes the surface represented by the quad to have a non-constant normal—specifically, every quad vertex can have a distinct normal vector. This is a simple approximation of a real smooth surface, whose normal would, in general, vary at every surface point. Gouraud shading applies the lighting model (Equation (2.1)) at every quad vertex, using the respective vertex normal, yielding potentially four different colors. Next, all quad pixels are rendered with a color that smoothly varies between the four vertex colors resulting from the shading, using a technique called _interpolation_. Interpolation is described in greater detail in Chapter 3. Figure 2.5 shows the result of Gouraud shading applied to the same dataset rendered in Figure 2.1 with flat shading. In OpenGL, the smooth shading mode is selected by the function call

```
glShadeModel(GL_SMOOTH);
```

![](img/1274306e378c42ed8a0ad5669902d2a1_46_0.png)

Figure 2.5. Elevation plot for the function \(f(x,y) = e^{-(x^2+y^2)}\) (Gouraud shaded).

To perform Gouraud shading, we must add vertex normal information to our Quad class. This is easily done by adding an extra method to this class:

```
void Quad::addNormal(float * n)
{
    glNormal3f(n[0], n[1], n[2]);
}
```

which specifies a normal vector \(\mathbf{n} = (n_x, n_y, n_z)\) for every quad vertex. In OpenGL, specifying a vector normal should be done before the specification of the vertex itself. In our case, `addNormal()` should be called right before `addVertex()` for that respective vertex.

The next step is to compute the actual vertex normals for our surface. The computing method depends on how the surface is specified. If the surface is specified analytically, e.g., by a function, we can proceed as follows. From analysis we know that a vector normal to the graph of \(f\), i.e., to our surface, is given by

\(\mathbf{n} = \left( -\frac{\partial f}{\partial x}, -\frac{\partial f}{\partial y}, 1 \right).\) (2.4)

The vector \(\mathbf{n}\) is related to another important mathematical concept called the *gradient*. Given a function \(f : \mathbb{R}^2 \to \mathbb{R}\), the gradient of \(f\), denoted \(\nabla f\), is the vector

\(\nabla f = \left( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right).\) (2.5)

```
float f(float, float); //the function to visualize
float* n(float, float); //the normal of f at (x,y)
for (float x=Xmin;x<Xmax-dx;x+=dx)
  for (float y=Ymin;y<Ymax-dy;y+=dy)
  {
    Quad q;
    q.addNormal(n(x,y));
    q.addPoint(f(x,y));
    q.addNormal(n(x+dx,y));
    q.addPoint(f(x+dx,y));
    q.addNormal(n(x+dx,y+dy));
    q.addPoint(f(x+dx,y+dy));
    q.addNormal(n(x,y+dy));
    q.addPoint(f(x,y+dy));
    q.draw();
  }
```

### Listing 2.4. Drawing a Gouraud-shaded height plot.

For functions with more variables, the gradient is defined analogously. Intuitively, the gradient of f is a vector that indicates, at every point in the domain of f, the direction in the domain in which f has the highest increase at that point. We shall encounter numerous applications of the gradient in the following chapters.

In our example, f(x,y) = e^(-(x^2+y^2)), so the vector v = (-2xf, -2yf, 1) has the same direction as the normal, though not the same length. We can thus compute the normal n by normalizing v:

\(\mathbf{n} = \left( \frac{-2xf}{\sqrt{4x^2f^2+4y^2f^2+1}} , \frac{-2yf}{\sqrt{4x^2f^2+4y^2f^2+1}} , \frac{1}{\sqrt{4x^2f^2+4y^2f^2+1}} \right) .\)
(2.6)

We can now draw the Gouraud-shaded height plot in Figure 2.5 using the code in Listing 2.4. Here, n is a function that computes the normal n of the original function f at a given point (x,y), i.e., implements Equation (2.6).

### Computing vertex normals

The normal computation method described previously works for any function for which we can compute its partial derivatives analytically, as in Equation (2.4). However, as discussed in Section 2.1, our function may not be specified analytically, but as a sampled dataset. Still, in practice, we can perform Gouraud shading of sampled (e.g., polygonal) datasets using a simple technique called normal averaging. For every sample point p_i, denote by P_1..P_N all polygons that have p_i as a vertex. We define the vertex normal n_i at p_i as the average of all polygon normals n(P_j) that have p_i as a
