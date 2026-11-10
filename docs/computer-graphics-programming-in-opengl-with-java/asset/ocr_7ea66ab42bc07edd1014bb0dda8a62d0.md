+   - `vn` – vertex normal
+   - `f` – face (typically vertices in a triangle)

Other tags make it possible to store the object name, materials it uses, curves, shadows, and many other details. We will limit our discussion to the four tags listed above, which are sufficient for importing a wide variety of complex models.

Suppose we use Blender to build a simple pyramid such as the one we developed for Program 4.3. Figure 6.14 is a screenshot of a similar pyramid being created in Blender.

![](bbox=[0.171, 0.337, 0.829, 0.646])

**Figure 6.14**
Pyramid built in Blender.

In Blender, if we now *export* our pyramid model, specify .obj format, and also set Blender to output texture coordinates and vertex normals, an OBJ file is created that includes all of this information. The resulting OBJ file is shown in Figure 6.15. (The actual values of the texture coordinates can vary depending on how the model is built.)

We have color-coded the important sections of the OBJ file for reference. The lines at the top beginning with “#” are comments placed there by Blender, which our importer ignores. This is followed by a line beginning with “o” giving the name of the object. Our importer can ignore this line as well. Later, there is a line