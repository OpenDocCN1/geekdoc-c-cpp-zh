+   5. Select (X,Y), (X,Z), or (Y,Z) as the texture coordinates, depending on which surface the collision occurred.

Program 16.6 shows the additions and changes to the Java/JOGL program and the compute shader. It textures the sphere with the earth image and the box with the brick image. The output is shown in Figure 16.7.

# Program 16.6 Adding Texture Coordinates

Java/JOGL Application

```
```java
...
private int earthTexture, brickTexture;                    // added to the top-level declarations
...
public void init(GLAutoDrawable drawable)
{
    ...
    brickTexture = Utils.loadTexture("code/brick1.jpg");
    earthTexture = Utils.loadTexture("code/earthmap1k.jpg");
}

public void display(GLAutoDrawable drawable)
{
    ...
    gl.glBindImageTexture(0, screenTextureID[0], 0, false, 0, GL_WRITE_ONLY, GL_RGBA8);

    gl.glActiveTexture(GL_TEXTURE1);
    gl.glBindTexture(GL_TEXTURE_2D, earthTexture);
    gl.glActiveTexture(GL_TEXTURE0);
    gl.glBindTexture(GL_TEXTURE_2D, brickTexture);
    gl.glActiveTexture(GL_TEXTURE0);             // reset of active texture is required when using
                                                // both image store and texture
    gl.glDispatchCompute(workGroupsX, workGroupsY, workGroupsZ);
    ...
}
```
```

Compute Shader

```
```glsl
...
layout (binding=1) uniform sampler2D sampEarth;
layout (binding=2) uniform sampler2D sampBrick;

...
struct Collision
{
    float t;    // value at which this collision occurs for a ray
    vec3 p;     // world position of the collision
```

```