computer rendering, but an actual photograph of an object, taken in the home of one of the authors.

There are two aspects to note about the shadow in Figure 8.16:

+   - The shadow is “softer” the further it is from the object and “harder” the closer it is to the object. This is apparent when comparing the shadow near the legs of the object versus the wider portion of the shadow at the right region of the image.
+   - The shadow appears slightly darker the closer it is to the object.

The dimensionality of the light source itself can lead to soft shadows. As shown in Figure 8.17, the various regions across the light source cast slightly different shadows. The lighter areas at the edges of the shadow — where only a portion of the light is blocked by the object — are collectively called the *penumbra*.

![](bbox=[0.614, 0.305, 0.857, 0.503])

# ### 3.5.7 Generating Soft Shadows – Percentage Closer Filtering (PCF)

There are various ways of simulating the penumbra effect to generate soft shadows in software. One of the simplest and most common is called *Percentage Closer Filtering* (PCF). In PCF (proposed in 1987 by Reeves et al. [RS87]), we sample the shadow texture at several surrounding locations to estimate what percentage of nearby locations are in shadow. Depending on how many of the nearby locations are in shadow, we increase or decrease the degree of lighting contribution for the pixel being rendered. The entire computation can be done in the fragment shader, and that is the only place where we have to change any code of the code. PCF also can be used to reduce jagged line artifacts.

Before we study the actual PCF algorithm, let's first look at a simple similar motivating example to illustrate the goal of PCF. Consider the set of output fragments (pixels) shown in Figure 8.18, whose colors are being computed by the fragment shader.

![](bbox=[0.671, 0.711, 0.857, 0.893])