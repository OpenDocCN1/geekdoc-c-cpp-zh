A few other minor details to note regarding Program 4.3:

+   - The variables pyrLocX, pyrLocY, and pyrLocZ need to be declared and then initialized in init() to the desired pyramid location, as was done for the cube location.
+   - The view matrix vMat is built at the top of display() and then used in both the cube’s and the pyramid’s model-view matrices.
+   - The vertex and fragment shaders are not shown—they are unchanged from Section 4.5.

# 4.8 MATRIX STACKS

So far, the models we have rendered have each been constructed of a single set of vertices. It is often desired, however, to build complex models by assembling smaller, simple models. For example, a model of a “robot” could be created by separately drawing the head, body, legs, and arms, where each of those is a separate model. An object built in this manner is often called a *hierarchical model*. The tricky part of building hierarchical models is keeping track of all the model-view matrices and making sure they stay perfectly coordinated—otherwise the robot might fly apart into pieces!

Hierarchical models are useful not only for building complex objects—they can also be used to generate complex scenes. For example, consider how our planet Earth revolves around the sun, and in turn how the moon revolves around the Earth. Such a scene is shown in Figure 4.11.⁵ Computing the moon’s actual

![](bbox=[0.18, 0.658, 0.82, 0.822])

**Figure 4.11**
Animated planetary system (sun and earth textures from [HT12], moon texture from [NA16]).

⁵ Yes, we know that the moon doesn’t revolve in this “vertical” trajectory around the earth, but rather in one that is more co-planar with the earth’s revolution around the sun. We chose this orbit to make our program’s execution clearer.