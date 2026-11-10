# Chapter 9

# # Sky and Backgrounds

+   9.1 Skyboxes — 221
+   9.2 Skydomes — 224
+   9.3 Implementing a Skybox — 226
+   9.4 Environment Mapping — 234
+   Supplemental Notes — 239

![](bbox=[0.441, 0.377, 0.583, 0.399])

The realism in a 3D scene can often be improved by generating a realistic effect at the distant horizon. As we look beyond our nearby buildings and trees, we are accustomed to seeing large distant objects such as clouds, mountains, or the sun (or at night, the moon and stars). However, adding such objects to our scene as individual models may come at an unacceptable performance cost. A *skybox* or *skydome* provides a relatively simple way of efficiently generating a convincing horizon.

# ## 9.1 Skyboxes

The concept of a *skybox* is a remarkably clever and simple one:

+   1. Instantiate a cube object.
+   2. Texture the cube with the desired environment.
+   3. Position the cube so it surrounds the camera.

We already know how to do all of these steps. There are a few additional details, however.

+   - *How do we make the texture for our horizon?*

A cube has six faces, and we will need to texture all of them. One way is to use six image files and six texture units. Another common (and efficient) way is to use a single image that contains textures for all six faces, such as shown in Figure 9.1.