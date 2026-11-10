This is often application specific—in our scenes, we will generally be pointing the camera from the light to the origin.

Several important details need to be handled in pass one:

+   - Configure the buffer and shadow texture.
+   - Disable color output.
+   - Build a look-at matrix from the light toward the objects in view.
+   - Enable the GLSL pass one shader program, containing only the simple vertex shader shown in Figure 8.5 that expects to receive an MVP matrix. In this case, the MVP matrix will include the object's model matrix M, the look-at matrix computed in the previous step (serving as the view matrix V), and the perspective matrix P. We call this MVP matrix "shadowMVP" because it is based on the point of view of the light rather than the camera. Since the view from the light isn't actually being displayed, the pass one shader program's fragment shader doesn't do anything.
+   - For each object, create the shadowMVP matrix and call glDrawArrays(). It is not necessary to include textures or lighting in pass one, because objects are not rendered to the screen.

```
```glsl
#version 430            // vertex shader
layout (location=0) in vec3 vertPos;
uniform mat4 shadowMVP;

void main(void)
{  gl_Position = shadowMVP * vec4(vertPos,1.0);
}
#version 430            // fragment shader
void main(void) {}
```
```

**Figure 8.5**
Shadow mapping pass 1 vertex and fragment shaders.

# ### 3.3.2 Shadow Mapping (Intermediate Step) – Copying the Z-Buffer to a Texture

OpenGL offers two methods for putting Z-buffer depth data into a texture unit. The first method is to generate an empty shadow texture and then use the command glCopyTexImage2D() to copy the active depth buffer into the shadow texture.