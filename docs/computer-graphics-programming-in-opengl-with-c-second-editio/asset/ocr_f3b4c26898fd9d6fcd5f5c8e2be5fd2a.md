+   - The perspective matrix is created once (in init()), using the screen window's width and height (and desired frustum parameters), and it usually remains unchanged unless the window is resized.

Generating model and view transformation matrices then happens in the display() function, as follows:

+   1. Build the view matrix based on the desired camera location and orientation.
+   2. For each model, do the following:
+       i. Build a model matrix based on the model's location and orientation.
+       ii. Concatenate the model and view matrices into a single "MV" matrix.
+       iii. Send the MV and projection matrices to the corresponding shader uniforms.

Technically, it isn't necessary to combine the model and view matrices into a single matrix. That is, they could be sent to the vertex shader in individual, separate matrices. However, there are certain advantages to combining them, while keeping the perspective matrix separate. For example, in the vertex shader, each vertex in the model is multiplied by the matrices. Since complex models may have hundreds or even thousands of vertices, performance can be improved by pre-multiplying the model and view matrices once before sending them to the vertex shader. Later, we will see the need to keep the perspective matrix separate for lighting purposes.

# 4.5 OUR FIRST 3D PROGRAM – A 3D CUBE

It's time to put all the pieces together! In order to build a complete C++/OpenGL/GLSL system to render our cube in a 3D "world," all of the mechanisms described so far will need to be put together and perfectly coordinated. We can reuse some of the code that we have seen previously in Chapter 2. Specifically, we won't repeat the following functions for reading in files containing shader code, compiling and linking them, and detecting GLSL errors; in fact, recall that we have moved them to a "Utils.cpp" file:

+   - createShaderProgram()
+   - readShaderSource()
+   - checkOpenGLError()
+   - printProgramLog()
+   - printShaderLog()