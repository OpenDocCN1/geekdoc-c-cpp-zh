![](bbox=[0.172, 0.092, 0.715, 0.423])

Figure 13.9 Scene with global lights calculated via deferred shading

# Adding Point Lights

Recall that one of the main reasons to use deferred shading is that it scales very well as the number of lights in the scene increases. This section discusses how to add support for many non-global lights.

Suppose the game has 100 different point lights. You could create a uniform array in the shader that stores all the information about these point lights, including position, color, radius, and so on. Then in the `GBufferGlobal.frag` shader code, you could loop over these point lights. Using the G-buffer sampled world position, you could figure out whether a fragment is within range of a point light and, if so, compute the Phong equation for this.