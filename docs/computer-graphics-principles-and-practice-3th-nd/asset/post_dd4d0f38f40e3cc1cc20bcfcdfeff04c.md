
to the radiance \(L_o\) passing through its center from the closest triangle. Radiance from farther triangles is not interesting because it will (conceptually) be blocked by the back of the closest triangle and never reach the image. The implementation of `sampleRayTriangle` appears in Listing 15.15.

To render the entire image, we must invoke `sampleRayTriangle` once for each pixel center and for each triangle. Listing 15.13 defines `rayTrace`, which performs this iteration. It takes as arguments a box within which to cast rays (see Section 15.4.4). We use \(L_o\) to denote the radiance from the triangle; the subscript “o” is for “outgoing”.

*Listing 15.13: Code to trace one ray for every pixel between \((x0, y0)\) and \((x1−1, y1−1)\), inclusive.*

```cpp
/** Trace eye rays with origins in the box from {x0, y0} to {x1, y1}.*/
void rayTrace(Image& image, const Scene& scene,
    const Camera& camera, int x0, int x1, int y0, int y1) {

    // For each pixel
    for (int y = y0; y < y1; ++y) {
        for (int x = x0; x < x1; ++x) {

            // Ray through the pixel
            const Ray& R = computeEyeRay(x + 0.5F, y + 0.5F, image.width(),
                                         image.height(), camera);

            // Distance to closest known intersection
            float distance = INFINITY;
            Radiance L_o;

            // For each triangle
            for (unsigned int t = 0; t < scene.triangleArray.size(); ++t){
                const Triangle& T = scene.triangleArray[t];

                if (sampleRayTriangle(scene, x, y, R, T, L_o, distance)) {
                    image.set(x, y, L_o);
                }
            }
        }
    }
}
```

To invoke `rayTrace` on the entire image, we will use the call:

```cpp
rayTrace(image, scene, camera, 0, image.width(), 0, image.height());
```

## 15.4.1 Generating an Eye Ray

Assume the camera’s center of projection is at the origin, \((0, 0, 0)\), and that, in the camera’s frame of reference, the y-axis points upward, the x-axis points to the right, and the z-axis points out of the screen. Thus, the camera is facing along its own \(-z\)-axis, in a right-handed coordinate system. We can transform any scene to this coordinate system using the transformations from Chapter 11.

We require a utility function, `computeEyeRay`, to find the ray through the center of a pixel, which in screen space is given by \((x + 0.5, y + 0.5)\) for integers \(x\) and \(y\). Listing 15.14 gives an implementation. The key geometry is depicted in Figure 15.3. The figure is a top view of the scene in which x increases to the right and z increases downward. The near plane appears as a horizontal line, and the start point is on that plane, along the line from the camera at the origin to the center of a specific pixel.

To implement this function we needed to parameterize the camera by either the image plane depth or the desired field of view. Field of view is a more intuitive way to specify a camera, so we previously chose that parameterization when building the scene representation.

Listing 15.14: Computing the ray through the center of pixel (x,y) on a width × height image.

```cpp
Ray computeEyeRay(float x, float y, int width, int height, const Camera& camera) {
    const float aspect = float(height) / width;

    // Compute the side of a square at z = -1 based on our
    // horizontal left-edge-to-right-edge field of view
    const float s = 2.0f * tan(camera.fieldOfViewX * 0.5f);

    const Vector3f start =
        Vector3f((x / width - 0.5f) * s,
                 -(y / height - 0.5f) * s * aspect, 1.0f) * camera.zNear;

    return Ray(start, start.direction());
}
```

We choose to place the ray origin on the near (sometimes called hither) clipping plane, at z = camera.zNear. We could start rays at the origin instead of the near plane, but starting at the near plane will make it easier for results to line up precisely with our rasterizer later.

The ray direction is the direction from the center of projection (which is at the origin, (0,0,0)) to the ray start point, so we simply normalize the start point.

> **Inline Exercise 15.6:** By the rules of Chapter 7, we should compute the ray direction as `(start - Vector3(0,0,0)).direction()`. That makes the camera position explicit, so we are less likely to introduce a bug if we later change the camera. This arises simply from strongly typing the code to match the underlying mathematical types. On the other hand, our code is going to be full of lines like this, and consistently applying correct typing might lead to more harm from obscuring the algorithm than benefit from occasionally finding an error. It is a matter of personal taste and experience (we can somewhat reconcile our typing with the math by claiming that `p.direction()` on a point `p` returns the direction to the point, rather than “normalizing” the point).
>
> Rewrite `computeEyeRay` using the distinct `Point` and `Vector` abstractions from Chapter 7 to get a feel for how this affects the presentation and correctness. If this inspires you, it's quite reasonable to restructure all the code in this chapter that way, and doing so is a valuable exercise.

![](img/f464cd0043eb5336aa0543fe20a0561b_455_0.png)

Figure 15.3. The ray through a pixel center in terms of the image resolution and the camera's horizontal field of view.

Note that the y-coordinate of the start is negated. This is because y is in 2D screen space, with a “y = down” convention, and the ray is in a 3D coordinate system with a “y = up” convention.

To specify the vertical field of view instead of the horizontal one, replace `fieldOfViewX` with `fieldOfViewY` and insert the line `s /= aspect`.

### 15.4.1.1 Camera Design Notes

The C++ language offers both functions and methods as procedural abstractions. We have presented `computeEyeRay` as a function that takes a `Camera` parameter to distinguish the “support code” `Camera` class from the ray-tracer-specific code that you are adding. As you move forward through the book, consider refactoring the support code to integrate auxiliary functions like this directly into the appropriate classes. (If you are using an existing 3D library as support code, it is likely that the provided camera class already contains such a method. In that case, it is worth implementing the method once as a function here so that you have the experience of walking through and debugging the routine. You can later discard your version in favor of a canonical one once you’ve reaped the educational value.)

A software engineering tip: Although we have chosen to forgo small optimizations, it is still important to be careful to use references (e.g., `Image&`) to avoid excess copying of arguments and intermediate results. There are two related reasons for this, and neither is about the performance of this program.

The first reason is that we want to be in the habit of avoiding excessive copying. A `Vector3` occupies 12 bytes of memory, but a full-screen `Image` is a few megabytes. If we’re conscientious about never copying data unless we want copy semantics, then we won’t later accidentally copy an `Image` or other large structure. Memory allocation and copy operations can be surprisingly slow and will bloat the memory footprint of our program. The time cost of copying data isn’t just a constant overhead factor on performance. Copying the image once per pixel, in the inner loop, would change the ray caster’s asymptotic run time from O(n) in the number of pixels to O(n²).

The second reason is that experienced programmers rely on a set of idioms that are chosen to avoid bugs. Any deviation from those attracts attention, because it is a potential bug. One such convention in C++ is to pass each value as a const reference unless otherwise required, for the long-term performance reasons just described. So code that doesn’t do so takes longer for an experienced programmer to review because of the need to check that there isn’t an error or performance implication whenever an idiom is not followed. If you are an experienced C++ programmer, then such idioms help you to read the code. If you are not, then either ignore all the ampersands and treat this as pseudocode, or use it as an opportunity to become a better C++ programmer.

### 15.4.1.2 Testing the Eye-Ray Computation

We need to test `computeEyeRay` before continuing. One way to do this is to write a unit test that computes the eye rays for specific pixels and then compares them to manually computed results. That is always a good testing strategy. In addition to that, we can visualize the eye rays. Visualization is a good way to quickly see the result of many computations. It allows us to more intuitively check results, and to identify patterns of errors if they do not match what we expected.

In this section, we’ll visualize the directions of the rays. The same process can be applied to the origins. The directions are the more common location for an error and conveniently have a bounded range, which make them both more important and easier to visualize.
