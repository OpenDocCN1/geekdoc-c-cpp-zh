
## 3.5 INTERPOLATION OF VERTEX ATTRIBUTES

It is important to understand how *vertex attributes* are processed in the OpenGL pipeline, versus how *uniform variables* are processed. Recall that immediately before the fragment shader is *rasterization*, where primitives (e.g., triangles) defined by vertices are converted to fragments. Rasterization *linearly interpolates vertex attribute values* so that the displayed pixels seamlessly connect the modeled surfaces.

By contrast, *uniform* variables behave like initialized constants and remain unchanged across each vertex shader invocation (i.e., for each vertex sent from the buffer). A uniform variable is not interpolated; it always contains the same value regardless of the number of vertices.

The interpolation done on vertex attributes by the rasterizer is useful in many ways. Later, we will use rasterization to interpolate colors, texture coordinates, and surface normals. It is important to understand that *all values sent through a buffer to a vertex attribute will be interpolated* further down the pipeline.

We have seen vertex attributes in a vertex shader declared as "in" to indicate that they receive values from a buffer. Vertex attributes may instead be declared as "out", meaning that they send their values forward toward the next stage in the pipeline. For example, the following declaration in a vertex shader specifies a vertex attribute named "color" that outputs a vec4:

```glsl
out vec4 color;
```

It is not necessary to declare an "out" variable for the vertex positions, because OpenGL has a built-in vec4 variable named gl_Position for that purpose. In the vertex shader, we apply the matrix transformations to the incoming vertex (declared earlier as position), assigning the result to gl_Position:

```glsl
gl_Position = proj_matrix * mv_matrix * position;
```

![](img/1695de1bc7486362f86c143285f3fb40_86_0.png)

The transformed vertices will then be automatically output to the rasterizer, with corresponding pixel locations ultimately sent to the fragment shader.

The rasterization process is illustrated in Figure 4.2. When specifying GL_TRIANGLES in the glDrawArrays() function, rasterization is done per triangle. Interpolation starts along the lines connecting the vertices, at a level of precision corresponding to the pixel display density. The pixels in the interior space of the triangle are then filled by interpolating along the horizontal lines connecting the edge pixels.

## 4.4 MODEL-VIEW AND PERSPECTIVE MATRICES

A fundamental step in rendering an object in 3D is to create appropriate transformation matrices and send them to uniform variables like we did in Section 4.2. We start by defining three matrices:

- 1. a *Model* matrix
- 2. a *View* matrix
- 3. a *Perspective* matrix

The *Model* matrix positions and orients the object in the world coordinate space. Each model has its own model matrix, and that matrix would need to be continuously rebuilt if the model moves.

The *View* matrix moves and rotates the models in the world to simulate the effect of a camera at a desired location. Recall from Chapter 2 that the OpenGL camera exists at location (0,0,0) and faces down the negative Z axis. To simulate the appearance of that camera being moved a certain way, we will need to move the objects themselves in the opposite direction. For example, moving a camera to the right would cause the objects in the scene to appear to move to the left; although the OpenGL camera is fixed, we can make it appear as though we have moved it to the right by moving the objects to the left.

The *Perspective* matrix is a transform that provides the 3D effect according to the desired frustum, as described earlier in Chapter 3.

It is also important to understand when to compute each type of matrix. Matrices that never change can be built in `init()`, but those that change would need to be built in `display()` so that they are rebuilt for each frame. Let's assume that the models are animated and the camera is movable. Then:

- A model matrix needs to be created *for each model* and *at each frame*.
- The view matrix needs to be created *once per frame* (because the camera can be moved), but it is the same for all objects rendered during that frame.
- The perspective matrix is created once (in init()), using the screen window's width and height (and desired frustum parameters), and it usually remains unchanged unless the window is resized.

Generating model and view transformation matrices then happens in the display() function, as follows:

- 1. Build the view matrix based on the desired camera location and orientation.
- 2. For each model, do the following:
    - i. Build a model matrix based on the model's location and orientation.
    - ii. Concatenate the model and view matrices into a single "MV" matrix.
    - iii. Send the MV and projection matrices to the corresponding shader uniforms.

Technically, it isn't necessary to combine the model and view matrices into a single matrix. That is, they could be sent to the vertex shader in individual, separate matrices. However, there are certain advantages to combining them, while keeping the perspective matrix separate. For example, in the vertex shader, each vertex in the model is multiplied by the matrices. Since complex models may have hundreds or even thousands of vertices, performance can be improved by pre-multiplying the model and view matrices once before sending them to the vertex shader. Later, we will see the need to keep the perspective matrix separate for lighting purposes.

## 4.5 OUR FIRST 3D PROGRAM – A 3D CUBE

It's time to put all the pieces together! In order to build a complete C++/OpenGL/GLSL system to render our cube in a 3D "world," all of the mechanisms described so far will need to be put together and perfectly coordinated. We can reuse some of the code that we have seen previously in Chapter 2. Specifically, we won't repeat the following functions for reading in files containing shader code, compiling and linking them, and detecting GLSL errors; in fact, recall that we have moved them to a "Utils.cpp" file:

- createShaderProgram()
- readShaderSource()
- checkOpenGLError()
- printProgramLog()
- printShaderLog()

```cpp
1.0f, -1.0f, -1.0f, 1.0f, -1.0f, 1.0f, 1.0f, -1.0f,
1.0f, -1.0f, 1.0f, 1.0f, 1.0f, 1.0f, -1.0f, 1.0f,
1.0f, -1.0f, 1.0f, -1.0f, -1.0f, 1.0f, 1.0f, 1.0f,
-1.0f, -1.0f, 1.0f, -1.0f, 1.0f, 1.0f, 1.0f, -1.0f,
-1.0f, -1.0f, 1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f,
-1.0f, 1.0f, -1.0f, -1.0f, 1.0f, -1.0f, 1.0f, 1.0f,
-1.0f, 1.0f, -1.0f, 1.0f, -1.0f, 1.0f, -1.0f, -1.0f,
1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f, 1.0f, -1.0f,
-1.0f, -1.0f, -1.0f, 1.0f, 1.0f, -1.0f, 1.0f, 1.0f,
1.0f, 1.0f, -1.0f, 1.0f, 1.0f, -1.0f, 1.0f, -1.0f
};

glGenVertexArrays(1, vao);
glBindVertexArray(vao[0]);
glGenBuffers(numVBOs, vbo);

glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertexPositions), vertexPositions, GL_STATIC_DRAW);
}

void init(GLFWwindow* window) {
    renderingProgram = Utils::createShaderProgram("vertShader.glsl", "fragShader.glsl");
    cameraX = 0.0f; cameraY = 0.0f; cameraZ = 8.0f;
    cubeLocX = 0.0f; cubeLocY = -2.0f; cubeLocZ = 0.0f;    // shift down Y to reveal perspective
    setupVertices();
}

void display(GLFWwindow* window, double currentTime) {
    glClear(GL_DEPTH_BUFFER_BIT);
    glUseProgram(renderingProgram);

    // get the uniform variables for the MV and projection matrices
    mvLoc = glGetUniformLocation(renderingProgram, "mv_matrix");
    projLoc = glGetUniformLocation(renderingProgram, "proj_matrix");

    // build perspective matrix
    glfwGetFramebufferSize(window, &width, &height);
    aspect = (float)width / (float)height;
    pMat = glm::perspective(1.0472f, aspect, 0.1f, 1000.0f); // 1.0472 radians = 60 degrees

    // build view matrix, model matrix, and model-view matrix
    vMat = glm::translate(glm::mat4(1.0f), glm::vec3(-cameraX, -cameraY, -cameraZ));
    mMat = glm::translate(glm::mat4(1.0f), glm::vec3(cubeLocX, cubeLocY, cubeLocZ));
    mvMat = vMat * mMat;
```
