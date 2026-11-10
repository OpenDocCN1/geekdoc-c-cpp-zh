the cube map at the camera location, while still allowing the synthetic camera to “look around.” The output of Program 9.2 is the same as for Program 9.1.

# Program 9.2 OpenGL Cube Map Skybox

C++/OpenGL application

```
~~~cpp
int brickTexture, skyboxTexture;
int renderingProgram, renderingProgramCubeMap;
...
void init(GLFWindow* window) {
    renderingProgram = Utils::createShaderProgram("vertShader.glsl", "fragShader.glsl");
    renderingProgramCubeMap = Utils::createShaderProgram("vertShader.glsl", "fragShader.glsl");
    setupVertices();

    brickTexture = Utils::loadTexture("brick1.jpg");       // for the torus in the scene
    skyboxTexture = Utils::loadCubeMap("cubeMap");         // folder containing the skybox textures
    glEnable(GL_TEXTURE_CUBE_MAP_SEAMLESS);
}

void display(GLFWindow* window, double currentTime) {
    // clear color and depth buffers, projection and camera view matrix as before.
    ...
    // draw cube map first – note that it now requires a different rendering program
    glUseProgram(renderingProgramCubeMap);

    // put the P and V matrices into their corresponding uniforms.
    ...
    // set up vertices buffer for cube (buffer for texture coordinates not necessary)
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);

    // make the cube map the active texture
    glActiveTexture(GL_TEXTURE0);
    glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);

    // disable depth testing, and then draw the cube map
    glEnable(GL_CULL_FACE);
    glFrontFace(GL_CCW);
    glDisable(GL_DEPTH_TEST);
    glDrawArrays(GL_TRIANGLES, 0, 36);
    glEnable(GL_DEPTH_TEST);
}
~~~
```