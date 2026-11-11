Figure 15.3. The figure is a top view of the scene in which x increases to the right and z increases downward. The near plane appears as a horizontal line, and the start point is on that plane, along the line from the camera at the origin to the center of a specific pixel.

To implement this function we needed to parameterize the camera by either the image plane depth or the desired field of view. Field of view is a more intuitive way to specify a camera, so we previously chose that parameterization when building the scene representation.

Listing 15.14: Computing the ray through the center of pixel (x,y) on a width × height image.

```
```cpp
Ray computeEyeRay(float x, float y, int width, int height, const Camera& camera) {
    const float aspect = float(height) / width;

    // Compute the side of a square at z = -1 based on our
    // horizontal left-edge-to-right-edge field of view
    const float s = -2.0f * tan(camera.fieldOfViewX * 0.5f);

    const Vector3f start =
        Vector3f((x / width - 0.5f) * s,
                 -(y / height - 0.5f) * s * aspect, 1.0f) * camera.zNear;

    return Ray(start, start.direction());
}
```
```

We choose to place the ray origin on the near (sometimes called hither) clipping plane, at z = camera.zNear. We could start rays at the origin instead of the near plane, but starting at the near plane will make it easier for results to line up precisely with our rasterizer later.

The ray direction is the direction from the center of projection (which is at the origin, (0,0,0)) to the ray start point, so we simply normalize start point.

> **Inline Exercise 15.6:** By the rules of Chapter 7, we should compute the ray direction as `(start - Vector3(0,0,0)).direction()`. That makes the camera position explicit, so we are less likely to introduce a bug if we later change the camera. This arises simply from strongly typing the code to match the underlying mathematical types. On the other hand, our code is going to be full of lines like this, and consistently applying correct typing might lead to more harm from obscuring the algorithm than benefit from occasionally finding an error. It is a matter of personal taste and experience (we can somewhat reconcile our typing with the math by claiming that `p.direction()` on a point `p` returns the direction to the point, rather than “normalizing” the point).
> >
> > Rewrite `computeEyeRay` using the distinct `Point` and `Vector` abstractions from Chapter 7 to get a feel for how this affects the presentation and correctness. If this inspires you, it's quite reasonable to restructure all the code in this chapter that way, and doing so is a valuable exercise.

![](bbox=[0.71, 0.67, 0.93, 0.85])

Figure 15.3. The ray through a pixel center in terms of the image resolution and the camera's horizontal field of view.

Note that the y-coordinate of the start is negated. This is because y is in 2D screen space, with a “y = down” convention, and the ray is in a 3D coordinate system with a “y = up” convention.