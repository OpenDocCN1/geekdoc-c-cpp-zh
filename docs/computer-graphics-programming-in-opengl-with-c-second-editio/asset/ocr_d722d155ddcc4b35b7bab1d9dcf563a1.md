![](bbox=[0.28, 0.14, 0.68, 0.47])

# ## 8.8 A SHADOW MAPPING EXAMPLE

Consider the scene in Figure 8.9 that includes a torus and a pyramid. A positional light has been placed on the left (note the specular highlights).

The pyramid *should* be casting a shadow on the torus.

![](bbox=[0.5, 0.57, 0.85, 0.76])

To clarify the development of the example, our first step will be to *render pass one to the screen* to make sure it is working properly. To do this, we will temporarily add a simple fragment shader (it will not be included in the final version) to pass one that just outputs a constant color (e.g., red); for example:

```
```glsl
#version 430
out vec4 fragColor;
void main(void)
{ fragColor = vec4(1.0, 0.0, 0.0, 0.0);
}
```
```