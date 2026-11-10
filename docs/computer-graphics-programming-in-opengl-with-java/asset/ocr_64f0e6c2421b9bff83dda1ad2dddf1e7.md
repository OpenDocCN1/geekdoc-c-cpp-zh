![](bbox=[0.14, 0.107, 0.853, 0.657])

**Figure 5.1**
Texturing a dolphin model with two different images [TU16].

# **5.1 LOADING TEXTURE IMAGE FILES**

There are a number of datasets and mechanisms that need to be coordinated to accomplish texture mapping efficiently in JOGL/GLSL:

+   - a *texture object* to hold the texture image (in this chapter we consider only 2D images)
+   - a special *uniform sampler* variable so that the vertex shader can access the texture
+   - a buffer to hold the *texture coordinates*