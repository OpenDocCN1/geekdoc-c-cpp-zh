Program 16.6 shows the additions and changes to the C++ program and the compute shader. It textures the sphere with the earth image and the box with the brick image. The output is shown in Figure 16.7.

# ### Program 16.6 — Adding Texture Coordinates

# #### C++/OpenGL Application

```
```cpp
...
GLuint earthTexture, brickTexture;      // added to the top-level declarations
...
void init(GLFWindow* window) {
    ...
    earthTexture = Utils::loadTexture("earthmap1k.jpg");
    brickTexture = Utils::loadTexture("brick1.jpg");
}
void display(GLFWindow* window, double currentTime) {
    glBindImageTexture(0, screenTextureID, 0, GL_FALSE, 0, GL_WRITE_ONLY, GL_RGBA8);
    glActiveTexture(GL_TEXTURE1);
    glBindTexture(GL_TEXTURE_2D, earthTexture);
    glActiveTexture(GL_TEXTURE2);
    glBindTexture(GL_TEXTURE_2D, brickTexture);
    glActiveTexture(GL_TEXTURE0);        // reset of active texture is required when using
                                         // both image store and texture
    glDispatchCompute(workGroupsX, workGroupsY, workGroupsZ);
    ...
}
```
```

# #### Compute Shader

```
```cpp
...
layout(binding=1) uniform sampler2D sampEarth;
layout(binding=2) uniform sampler2D sampBrick;
...
struct Collision
{ float t;          // value at which this collision occurs for a ray
  vec3 p;           // world position of the collision
  vec3 n;           // normal of the collision
  bool inside;      // whether the collision occurs inside of the object
  int object_index; // index of the object this collision hit
```
```