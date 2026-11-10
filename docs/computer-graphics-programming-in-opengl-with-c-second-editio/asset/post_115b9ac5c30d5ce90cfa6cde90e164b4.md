
The setupVertices() function sets up the VAO and two VBOs (although only one is used) and loads the cube vertices into the 0th VBO buffer.

Note that the init() function performs tasks that only need to be done once: reading in shader code and building the rendering program, and loading cube vertices into the VBO (by calling setupVertices()). Note that it also positions the cube and the camera in the world. Later we will animate the cube and also see how to move the camera around, at which point we may need to remove this hardcoded positioning.

Now let’s look at the display() function. Recall that display() may be called repeatedly and the rate at which it is called is referred to as the *frame rate*. That is, animation works by continually drawing and redrawing the scene, or frame, very quickly. It is usually necessary to clear the depth buffer before rendering a frame so that hidden surface removal occurs properly (not clearing the depth buffer can sometimes result in every surface being removed, resulting in a completely black screen). By default, depth values in OpenGL range from 0.0 to 1.0. Clearing the depth buffer is done by calling glClear(GL_DEPTH_BUFFER_BIT), which fills the depth buffer with the default value (usually 1.0).

Next, display() enables the shaders by calling glUseProgram(), installing the GLSL code on the GPU. Recall this doesn’t run the shader program, but it does enable subsequent OpenGL calls to determine the shader’s *vertex attribute* and *uniform* locations. The display() function next gets the uniform variable locations, builds the perspective, view, and model matrices³, concatenates the view and model matrices into a single MV matrix, and assigns the perspective and MV matrices to their corresponding uniforms. Here, it is worth noting also the form of the GLM call to the translate() function:

```cpp
vMat = glm::translate(glm::mat4(1.0f), glm::vec3(-cameraX, -cameraY, -cameraZ));
```

The somewhat cryptic-looking call builds a translation matrix by (a) starting with an identity matrix (using the glm::mat4(1.0f) constructor) and (b) specifying translation values in the form of a vector (with the glm::vec3(x,y,z) constructor). Many of the GLM transform operations utilize this approach.

³ An astute reader may notice that it shouldn’t be necessary to build the perspective matrix every time display() is called, because its value doesn’t change. This is partially true—the perspective matrix would need to be recomputed if the user were to resize the window while the program was running. In Section 4.11 we will handle this situation more efficiently, and in the process we will move the computation of the perspective matrix out of display() and into the init() function.

Next, display() enables the buffer containing the cube vertices and attaches it to the 0th vertex attribute to prepare for sending the vertices to the shader.

The last thing display() does is draw the model by calling glDrawArrays(), specifying that the model is composed of triangles and has 36 total vertices. The call to glDrawArrays() is typically preceded by additional commands that adjust rendering settings for this model.⁴ In this example there are two such commands, both of which are related to depth testing. Recall from Chapter 2 that depth testing is used by OpenGL to perform hidden surface removal. Here, we enable depth testing and specify the particular depth test we wish OpenGL to use. The settings shown here correspond to the description in Chapter 2; later in the book we will see other uses for these commands.

⁴ Often, these calls may be placed in init() rather than in display(). However, it is necessary to place one or more of them in display() when drawing multiple objects with different properties. For simplicity, we always place them in display().

Finally, consider the shaders. First, note that they both include the same block of uniform variable declarations. Although this is not always required, it is often a good practice to include the same block of uniform variable declarations in all of the shaders within a particular rendering program.

Note also in the vertex shader the presence of the layout qualifier on the incoming vertex attribute position. Since the location is specified as “0”, the display() function can reference this variable simply by using 0 in the first parameter of the glVertexAttribPointer() function call and in the glEnableVertexAttribArray() function call. Note also that the position vertex attribute is declared as a vec3, and so it needs to be converted to a vec4 in order to be compatible with the 4x4 matrices with which it will be multiplied. This conversion is done with vec4(position,1.0), which builds a vec4 out of the variable named “position”, putting a value of 1.0 in the newly added 4th spot.

The multiplication in the vertex shader applies the matrix transforms to the vertex, converting it to camera space (note the right-to-left concatenation order). Those values are put in the built-in OpenGL output variable gl_Position, and then proceed through the pipeline and are interpolated by the rasterizer.

The interpolated pixel locations (referred to as fragments) are then sent to the fragment shader. Recall that the primary purpose of the fragment shader is to set the color of an outputted pixel. In a manner similar to the vertex shader, the fragment shader processes the pixels one by one, with a separate invocation for each pixel. In this case, it outputs a hardcoded value corresponding to red. For reasons indicated earlier, the uniform variables have been included in the fragment shader even though they aren’t being used there in this example.

An overview of the flow of data starting with the C++/OpenGL application and passing through the pipeline is shown in Figure 4.5.

![](img/1695de1bc7486362f86c143285f3fb40_95_0.png)

Let’s make a slight modification to the shaders. In particular, we will assign a color to each vertex according to its location, and put that color in the outgoing vertex attribute varyingColor. The fragment shader is similarly revised to accept the incoming color (interpolated by the rasterizer) and use that to set the color of the output pixel. Note that the code also multiplies the location by 1/2 and then adds 1/2 to convert the range of values from [-1..+1] to [0..1]. Note also the use of the common convention of assigning variable names that include the word “varying” to programmer-defined interpolated vertex attributes. The changes in each shader are highlighted, and the resulting output is as follows.

### Revised vertex shader:

```glsl
#version 430

layout (location=0) in vec3 position;
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;

out vec4 varyingColor;

void main(void)
{
    gl_Position = proj_matrix * mv_matrix * vec4(position,1.0);
    varyingColor = vec4(position,1.0) * 0.5 + vec4(0.4, 0.5, 0.5, 0.5);
}
```

### Revised fragment shader:

```glsl
#version 430
in vec4 varyingColor;
out vec4 color;
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;

void main(void)
{
    color = varyingColor;
}
```

![](img/1695de1bc7486362f86c143285f3fb40_96_0.png)

**Figure 4.6**  
Cube with interpolated colors.

Note that because the colors are sent out from the vertex shader in a vertex attribute (*varyingColor*), *they too are interpolated* by the rasterizer! The effect of this can be seen in Figure 4.6, where the colors from corner to corner are clearly interpolated smoothly throughout the cube.

Note also that the “out” variable varyingColor in the vertex shader is also the “in” variable in the fragment shader. The two shaders know which variable from the vertex shader feeds which variable in the fragment shader because they have the same name “varyingColor” in both shaders.

Since our main() includes a render loop, we can animate our cube as we did in Program 2.6, by building the model matrix using a varying translation and rotation
