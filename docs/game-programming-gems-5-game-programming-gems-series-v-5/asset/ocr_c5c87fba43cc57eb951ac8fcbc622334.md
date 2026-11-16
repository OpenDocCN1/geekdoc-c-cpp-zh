![](bbox=[0.21, 0.08, 0.89, 0.4])

![](bbox=[0.21, 0.43, 0.9, 0.73])

impostors updated every frame instead of static sprites successfully eliminates this problem.

In the stage of impostor rendering, depth and color information are stored in target textures. The result is a 2.5 dimensional impostor. The z-near and z-far planes are adjusted to approximate a reasonable bounding box for the rendered group of leaves, as shown in Figure 5.4.6. In the final phase of rendering, the stored depth values are