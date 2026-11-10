Figure 16.15 shows the result. Notice that the view of the scene through the transparent sphere has been flipped and appears upside down. A flipped (and severely curved) version of the brick box is also visible in the sphere, as is the checkerboard plane. Also, although not easily seen in Figure 16.15, it is the *back* of the skybox that is visible in the sphere, whereas in Figure 16.11, the sphere reflected the front portion of the skybox.

![](bbox=[0.301, 0.253, 0.703, 0.583])

**Figure 16.15**
Output of Program 16.10, showing refraction through a solid transparent sphere.

# ### 16.3.3 Combining Reflection, Refraction, and Textures

Transparent objects are also usually slightly reflective. Combining reflection and refraction (as well as textures) can be done in a similar manner as combining lighting and textures, as we did in Chapter 7. That is, we can simply build a weighted sum of whichever elements our objects incorporate.

In Program 16.11, the raytrace() function generates both reflection and refraction rays, combining them using a weighted sum. The degree to which the object is reflective rather than transparent can be tuned by adjusting the weights to get various effects. In this example, we have also replaced the skybox with a blue room box to make the specific effects of reflection and refraction more clearly