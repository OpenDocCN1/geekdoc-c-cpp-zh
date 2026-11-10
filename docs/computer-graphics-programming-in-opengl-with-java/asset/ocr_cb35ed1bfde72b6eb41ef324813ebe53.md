distortion. Since different headset lenses can have different properties, this *distortion correction* would ideally be tunable for different headsets.

Measuring and correcting lens distortion is complex, and a full study is beyond the scope of this book. Instead we walk through the steps for a typical example. Specifically, we apply a barrel distortion correction to our fog example, roughly tuned for the Google Cardboard headset. We also point out some of the tunable parameters along the way. More thorough coverage can be found on the Internet [BS16].

Applying a distortion correction to a rendered scene can be done in a variety of ways. One of the most efficient methods is called *vertex displacement*, in which the elements in the scene are each rendered with the desired distortion correction applied to the vertices [BS16]. For purposes of simplicity, in this chapter we use an easier, albeit less efficient, *fragment-shader-based* approach. The steps are as follows:

+   1. Render the entire scene to a framebuffer texture, from the left eye point of view.
+   2. Use the texture to render a rectangular region to the left half of the screen (the fragment shader applies barrel distortion in this step).
+   3. Repeat the process for the right eye, to the right half of the screen.

We have already studied how to render a scene to a framebuffer texture, for example, when we studied shadows. We have just learned how to render to the left and right halves of the screen using `glViewport()`. Now we need to learn how to take a framebuffer texture and render it while distorting the image it contains.

Rendering (and texturing) a rectangular object should by now be a simple matter, using six vertices comprising two triangles. Applying a corresponding texture would then typically be done in the fragment shader using the `texture()` function, which expects parameters for the *X* and *Y* texture coordinates. Since our rectangle fills the entire viewport, an *undistorted* rendering would be achieved by simply scaling the texture coordinates to the viewport dimensions, such as

```
```
fragColor = texture(gl_FragCoord.x / (sizeX/2), gl_FragCoord.y / sizeY);
```
```

Instead, we need to modify the *X* and *Y* texture lookup values so that they access a different texel, specifically the one that would be at that location (X,Y) if the texture were barrel-distorted. The mathematical derivation of barrel distortion