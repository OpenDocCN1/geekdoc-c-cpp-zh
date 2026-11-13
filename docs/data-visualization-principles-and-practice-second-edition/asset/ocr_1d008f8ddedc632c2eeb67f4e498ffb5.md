Hence, to create the height plot shown in Figure 2.1, it is sufficient to issue a single `glColor3f` call before all the quads are drawn. The green color shown in the figure corresponds to the setting \( r = 0.3 \), \( g = 0.8 \), \( b = 0.37 \).

Besides specifying the object color, we must specify the light intensity and direction, i.e., the parameters \( I_l \) and \( \mathbf{L} \) in Equation (2.1). In OpenGL, lights are specified by a number of function calls. First, OpenGL must be set up to use the Phong lighting equation, by enabling the lighting mechanism. OpenGL supports several light sources (most implementations provide at least eight of them). The next step is to enable one of the light sources, say the first one. These two operations are accomplished by the function calls

```
gEnable(GL_LIGHTING);
gEnable(GL_LIGHT0);
```

After lighting and the desired light(s) are enabled, we can specify the light intensity model. As explained in the previous section, OpenGL uses a three-component light model, so the Phong lighting model (Equation (2.1)) is applied three times. Moreover, OpenGL allows us to separately specify the amount of light that interacts with the ambient, diffuse, and specular material components. Putting it all together, the lighting equations used by OpenGL are

\( I^R(p, \mathbf{v}, \mathbf{L}) = I^R_{amb}c^R_{amb} + I^R_{diff}c^R_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^R_{spec}c^R_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,,\)
\( I^G(p, \mathbf{v}, \mathbf{L}) = I^G_{amb}c^G_{amb} + I^G_{diff}c^G_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^G_{spec}c^G_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,,\) (2.3)
\( I^B(p, \mathbf{v}, \mathbf{L}) = I^B_{amb}c^B_{amb} + I^B_{diff}c^B_{diff} \max(-\mathbf{L} \cdot \mathbf{n}, 0) + I^B_{spec}c^B_{spec} \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha \,.\)

Here, the superscripts \( R \), \( G \), and \( B \) denote the color components. The triplet \( (I^R_{amb}, I^G_{amb}, I^B_{amb}) \) specifies the amount (intensity) of light that interacts with the ambient material component \( (c^R_{amb}, c^G_{amb}, c^B_{amb}) \), and is specified by the function call

```
gLightfv(GL_LIGHT0, GL_AMBIENT, I);
```

Here, \( I = (I^R_{amb}, I^G_{amb}, I^B_{amb}) \) is a vector of three floating-point values. The same function can be used to specify the diffuse and specular light intensities for all