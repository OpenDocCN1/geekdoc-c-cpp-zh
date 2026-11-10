Program 16.7, with and without ADS lighting applied to the skybox (ADS lighting is applied to the other objects). Comparing figures 16.8 and 16.9 illustrates why lighting effects are generally appropriate for room boxes, but not for skyboxes.

![](bbox=[0.143, 0.202, 0.854, 0.494])

**Figure 16.9**
Output of Program 16.7 with and without ADS lighting applied to a skybox

# ## 16.2.10 Plane Intersection and Procedural Textures

In the previous examples, textures were provided in the form of texture image files. In some cases, a surface texture is sufficiently simple that it can be created procedurally, with the advantage that such textures are less likely to exhibit image-related artifacts.

In Program 16.8, we add a plane object (more precisely, a plane segment) to the scene, serving as a sort of table-top surface below the objects. Shadows are cast onto the plane object, but not onto the skybox. The plane has been textured with a checkerboard pattern, generated procedurally.

Computing the intersection point of a ray with a plane is significantly easier than it was for the sphere and the box because a plane has no “inside” that needs to be considered, so there is always at most one intersection point to consider. The derivation is well documented [§16]. Using standard geometry, the distance $t$ along a ray starting at position with direction when it intersects a horizontal plane centered at the origin with normal $n_p=(0,1,0)$ is: