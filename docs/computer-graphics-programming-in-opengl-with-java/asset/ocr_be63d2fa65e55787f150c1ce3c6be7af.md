When building a 3D model of an object, we generally orient the model in the most convenient manner for describing it. For example, when modeling a sphere, we might orient the model with the sphere's center at the origin (0,0,0) and give it a convenient radius, such as 1. The space in which a model is defined is called its *local space*, or *model space*. OpenGL documentation uses the term *object space*.

The sphere might then be used as a piece of a larger model, such as becoming the head on a robot. The robot would, of course, be defined in its own local/model space. Positioning the sphere model into the robot model space can be done using the matrix transforms for scale, rotation, and translation, as illustrated in Figure 3.9. In this manner, complex models can be built hierarchically (this is developed further in Section 4.8 of Chapter 4, using a stack of matrices).

![](bbox=[0.27, 0.452, 0.745, 0.596])

In the same manner, modeled objects are placed in a simulated world by deciding on the orientation and dimensions of that world, called *world space*. The matrix that positions and orients an object into world space is called a *model matrix*, or **M**.

# ## 3.7 EYE SPACE AND THE SYNTHETIC CAMERA

So far, the transform matrices we have seen all operate in 3D space. Ultimately, however, we will want to display our 3D space—or a portion of it—on a 2D monitor. In order to do this, we need to decide on a vantage point. Just as we see our real world through our eyes from a particular point, in a particular direction, so too must we establish a position and orientation as the window into our virtual world. This vantage point is called “view” or “eye” space, or the “synthetic camera.”