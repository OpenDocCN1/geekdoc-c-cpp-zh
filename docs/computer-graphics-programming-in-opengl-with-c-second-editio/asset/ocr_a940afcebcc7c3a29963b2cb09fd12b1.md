Now is an appropriate time to take a closer look at the OpenGL calls in Program 2.1. Consider this one:

```
glClear(GL_COLOR_BUFFER_BIT);
```

In this case, the OpenGL function being called, as described in the OpenGL reference documentation (available on the web at https://www.opengl.org/sdk/docs), is:

```
void glClear(GLbitfield mask);
```

The parameter references a “GLbitfield” called “GL_COLOR_BUFFER_BIT”. OpenGL has many predefined constants (some of them are called *enums*); this one references the *color buffer* that contains the pixels as they are rendered. OpenGL has several color buffers, and this command clears all of them—that is, it fills them with a predefined color called the “clear color.” Note that “clear” in this context doesn’t mean “a color that is clear”; rather, it refers to the color that is applied when a color buffer is reset (cleared).

Immediately before the call to glClear() is a call to glClearColor(). This allows us to specify the value placed in the elements of a color buffer when it is cleared. Here we have specified (1,0,0,1), which corresponds to the RGBA color *red*.

Finally, our render loop exits when the user attempts to close the GLFW window. At that time, our main() asks GLFW to destroy the window and terminate, via calls to glfwDestroyWindow() and glfwTerminate() respectively.

# 2.1.2 Vertex and Fragment Shaders

Our first OpenGL program didn’t actually draw anything—it simply filled the color buffer with a single color. To actually draw something, we need to include a *vertex shader* and a *fragment shader*.

You may be surprised to learn that OpenGL is capable of drawing only a few kinds of very simple things, such as *points, lines,* or *triangles*. These simple things are called *primitives*, and for this reason, most 3D models are made up of lots and lots of primitives, usually triangles.

Primitives are made up of *vertices*—for example, a triangle consists of three vertices. The vertices can come from a variety of sources—they can be read from files and then loaded into buffers by the C++/OpenGL application, or they can be hardcoded in the C++ code or even in the GLSL code.