![](bbox=[0.194, 0.114, 0.809, 0.337])

**Figure 14.1**
Fog blending based on distance.

There are a variety of methods for simulating fog, from very simple ones to sophisticated models that include light scattering effects. However, even very simple approaches can be effective. One such method is to blend the actual pixel color with another color (the “fog” color, typically gray or bluish-gray—also used for the background color), based on the distance the object is from the eye.

Figure 14.1 illustrates the concept. The eye (camera) is shown at the left, and two red objects are placed in the view frustum. The cylinder is closer to the eye, so it is mostly its original color (red); the cube is further from the eye, so it is mostly fog color. For this simple implementation, virtually all of the computations can be performed in the fragment shader.

Program 14.1 shows the relevant code for a very simple fog algorithm that uses a linear blend from object color to fog color based on the distance from the camera to the pixel. Specifically, this example adds fog to the height mapping example from Program 10.4.

# **Program 14.1 Simple Fog Generation**

*Vertex shader*

```
...
out vec3 vertEyeSpacePos;
...
// Compute vertex position in eye space, without perspective, and send it to the fragment shader.
// The variable "p" is the height-mapped vertex, as described earlier in Program 10.4.
vertEyeSpacePos = (mv_matrix * p).xyz;
```